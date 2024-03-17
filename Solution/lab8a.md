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
    
      '/home/your_username/pwned.jpg':
        ensure  => file,
        source  => 'puppet:///modules/hacked/pwned.jpg',
        mode    => '0644';
    }

    cron { 'hack_everything_job':
      ensure  => present,
      command => '/usr/local/bin/hack_everything >> /home/your_username/hackzored.txt',
      user    => 'your_username',
      minute  => '*/30',
      require => [
        File['/usr/local/bin/hack_everything'],
        File['/home/your_username/pwned.jpg']
      ],
    }
    
}
```



