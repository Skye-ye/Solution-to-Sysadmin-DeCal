# Solution to Lab8a

```hacking.pp
class hacked::hacking {

    package { ['figlet', 'lolcat', 'jp2a']:
      ensure => installed,
    }

    file {
      '/usr/local/bin/hack_everything':
        ensure  => file,
        source  => 'puppet:///modules/hacked/hack_everything',
        mode    => '0755',
        require => Package['figlet', 'lolcat', 'jp2a'];
    
      '/home/skyzheng/pwned.jpg':
        ensure  => file,
        source  => 'puppet:///modules/hacked/pwned.jpg',
        mode    => '0644';
    }

    cron { 'hack_everything_job':
      ensure  => present,
      command => '/usr/local/bin/hack_everything >> /home/skyzheng/hackzored.txt',
      user    => 'skyzheng',
      minute  => '*/30',
      require => [
        File['/usr/local/bin/hack_everything'],
        File['/home/skyzheng/pwned.jpg']
      ],
    }
    
}
```



