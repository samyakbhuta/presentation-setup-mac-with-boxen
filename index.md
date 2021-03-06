### Boxen from Github

> QUIT WORRYING ABOUT YOUR TOOLS.

[https://boxen.github.com](https://boxen.github.com)



### But why we need tools ?


TODO: Write something for this slide. We are artist. Lest, we are humans. We are where we are cause of tool. May be a video. May be quotation.

The objective of this slide is to make sure audience understands why tooling is such an important thing.



### Boxen from Github

> Automate the pain out of your development environment. Boxen installs your dependencies so you can focus on getting things done.

[https://boxen.github.com](https://boxen.github.com)


### It is just puppetry!

> Boxen is basically a customised-for-Mac wrapper round the provisioning tool Puppet

[http://cookieshq.co.uk/posts/adventures-with-boxen/](http://cookieshq.co.uk/posts/adventures-with-boxen/)


### Why we need it ?

* List features as told by Boxen's own homepage.
* Not everybody (even developers) will be in position to appreciate why those features matter. Explaining the importance of these in details. Providing more empirical proof and testimonials will help.


### Benefits

* Eventhough discussing each feature will imply discussing the benefits as well. A nice *list* of benefits will help us reinforce the idea and let them really root for it. Also, setting the charge and the pace and keep them interested for the entire presentation.


### Underlying Opinion

> We believe that development is production, so we value consistency, predictability, and reproducibility over artisanal, hand-tweaked development environments.


###  Community

* Lots of [third party modules](https://github.com/boxen)
* Create your own modules and extend


### You know Puppet ?

* Boxen uses [Puppet](https://puppetlabs.com/)
* Benefit withPuppet is that all its changes are idempotent, and so unlike a shell script, stuff shouldn't break if you re-run it!



### Let's start it

* Create a project manifest. Run a command. That's it.


### Checklist

* TODO : Make sure the pre-requisites of installing boxen are met.
```
Boxen only works on Macs
Boxen requires the Xcode Command Line Tools to be installed.
Boxen will not work with an existing rvm install.
Boxen may not play nice with a GitHub username that includes a dash(-)
Boxen may not play nice with an existing rbenv install.
Boxen may not play nice with an existing chruby install.
Boxen may not play nice with an existing homebrew install.
Boxen may not play nice with an existing nvm install.
Boxen recommends installing full Xcode.
```


### Create a new git repo

* You can fork, but then you might want to have this all private.


### Perform following steps : Bootstrapping Steps

```
sudo mkdir -p /opt/boxen
sudo chown ${USER}:staff /opt/boxen
git clone https://github.com/boxen/our-boxen /opt/boxen/repo
cd /opt/boxen/repo
git remote rm origin
git remote add origin <the location of my new git repository>
git push -u origin master
```


### Installing the Configuration

```
cd /opt/boxen/repo
./script/boxen
```

In case you don't want to have your harddrive in Full Encryption Mode, follow the last command with an option.

```
./script/boxen --no-fde
```


### Will Prompt for
* For installing ```bundler```
* For Github username and password


### Installation will take time
* There will be lot of the things that will be downloaded. Have a coffee !


### We need to update our shell config

* Update ```~/.bashrc``` or ```~/.zshrc``` or ```~/.profile``` with ...

  ```
  [ -f /opt/boxen/env.sh ] && source /opt/boxen/env.sh
  ```



### Customize your environment

* We will start by putting more brew packages that we think we need.
* Let's start with ```cowsay``` command line tool.
* With Brew, it would be install with command ```brew install cowsay```.


### Customize your environment - 2
* In case of Boxen, we will still fetch the command using brew package system.
* But, we will not do it manually, and just ask Boxen to do this bit for us.


### Adding more brew packages
* Open the file ```site.pp``` in ```repo/manifests``` folder.
* Find following bit of code

  ```
  # common, useful packages
  package {
    [
      'ack',
      'findutils',
      'gnu-tar'
    ]:
  }

  ```
* Add ```cowsay``` as additional package in the array list.


### Install it using Boxen
* Now, just go to commnad line and type the command ```boxen```
* It will install the ```cowsay``` package
* Test it with ```cowsay 'Hello World'```


### Let's also install Google Chrome
* Add ```github "chrome",  "1.2.0"```` at the end of ```Puppetfile```.
* Add ```include chrome``` at ```site.pp``` file. The file will be something like following.

  ```
  node default {
    # ...
    # other code
    # ...

    include chrome
  }
  ```


### Why not also install iTerm?
* Add ```github "iterm2",  "1.2.0"``` at the end of ```Puppetfile```.
* Add ```include iterm2::stable``` at ```site.pp``` file. The file will be something like following.

  ```
  node default {
    # ...
    # other code
    # ...

    include iterm2::stable
  }
  ```


### But, what about my favorite color scheme ?
* Boxen is not all about putting binary executables. It has much more wider scope.
* Here, we will also install few color schemes that boxen provides us.
* Update ```site.pp``` file with following code snippet. Put it right after, ```include iterm2::stable```.

  ```
  include iterm2::colors::arthur
  include iterm2::colors::saturn
  include iterm2::colors::solarized_light
  include iterm2::colors::solarized_dark
  ```


### How about adding node modules ?
* Boxen allows you to install node modules for each version of node.
* Let's add coffeescript module (globally!) in our system.
* Let's us also add yeoman command line tool.
* Update ```site.pp``` file with following code snippet.

  ```
  # Node.js Modules
  $nodejs_modules = [
    'coffee-script',
    'yo'
  ]

  nodejs::module { $nodejs_modules :
    node_version => 'v0.10',
  }

  ```



### Adding Personal Taste - 1
* Create a manifest file that lists things that you want.
  ```
  touch  modules/people/manifests/<your_github_id>.pp
  ```
* Copy following code
  ```
  class people::samyakbhuta {
    include emacs   # requires emacs module in Puppetfile
  }
  ```
* This will install emacs on your system.


### Adding Personal Taste - 2
* Let's also have our personal repo cloned, and in folder we want.
* Add following code.
  ```
  $home     = "/Users/${::boxen_user}"
  $forksdir = "${home}/Forks"
  $repo_name = "${forksdir}/<repo_name>"

  file { $forksdir:
    ensure  => directory
  }

  repository { $repo_name:
    source  => '<your_github_id>/<repo_name>',
    require => File[$forksdir]
  }
  ```
* Run ```boxen```.



### Adding Projects
* TODO


### Pretedning Boxen
* ```boxen --pretend```


### Sharing your boxen setup with others
* You can make it public and other can just start with your repo
* Use [boxen-web](https://github.com/boxen/boxen-web) to allow access to your boxen setup over the web
