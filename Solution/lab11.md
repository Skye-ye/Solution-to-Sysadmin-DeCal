# Solution to Lab11

`Minecraft.pp`:

```
user { 'minecraft':
  ensure     => present,
  managehome => true,
  home       => '/home/minecraft',
}

file { '/home/minecraft':
  ensure  => 'directory',
  owner   => 'minecraft',
  group   => 'minecraft',
  require => User['minecraft'],
}

package { 'default-jre':
  ensure => installed,
}

file { '/home/minecraft/server.properties':
  ensure  => file,
  owner   => 'minecraft',
  group   => 'minecraft',
  source  => '/path/to/server.properties',
  require => User['minecraft'],
}

file { '/home/minecraft/eula.txt':
  ensure  => file,
  owner   => 'minecraft',
  group   => 'minecraft',
  content => 'eula=true',
  require => User['minecraft'],
}

file { '/home/minecraft/server.jar':
  ensure  => file,
  owner   => 'minecraft',
  group   => 'minecraft',
  source  => 'https://launcher.mojang.com/v1/objects/3dc3d84a581f14691199cf6831b71ed1296a9fdf/server.jar',
  require => User['minecraft'],
}

$memory_available = '2048M'

file { '/etc/systemd/system/minecraft.service':
  ensure  => file,
  owner   => 'root',
  group   => 'root',
  mode    => '0644',
  content => template('/path/to/minecraft.service.erb'),
  require => User['minecraft'],
}

service { 'minecraft':
  ensure   => running,
  enable   => true,
  provider => 'systemd',
  require  => File['/etc/systemd/system/minecraft.service'],
}

file { '/home/minecraft/backups':
  ensure => 'directory',
  owner  => 'minecraft',
  group  => 'minecraft',
}

file { '/home/minecraft/backup.sh':
  ensure  => 'file',
  owner   => 'minecraft',
  group   => 'minecraft',
  mode    => '0755', # Make the script executable
  content => "#!/bin/sh\ncp -r /home/minecraft/world \"/home/minecraft/backups/world-$(date -Is)\"",
}

cron { 'minecraft_backup':
  user     => 'minecraft',
  command  => '/home/minecraft/backup.sh',
  minute   => '*',
  require  => File['/home/minecraft/backup.sh'], 
}

exec { 'create_swapfile':
  command => 'dd if=/dev/zero of=/swapfile bs=2M count=2048',
  path    => ['/bin', '/usr/bin'],
  unless  => 'test -f /swapfile', 
}

exec { 'enable_swap':
  command => 'mkswap /swapfile && swapon /swapfile',
  path    => ['/sbin', '/bin', '/usr/sbin', '/usr/bin'],
  unless  => 'swapon -s | grep -q /swapfile', 
  require => Exec['create_swapfile'], 
}
```

