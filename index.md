### Boxen from Github

> QUIT WORRYING ABOUT YOUR TOOLS.

[https://boxen.github.com](https://boxen.github.com)


### But why we need tools ?


TODO: Write something for this slide. We are artist. Lest, we are humans. We are where we are cause of tool. May be a video. May be quotation.

The objective of this slide is to make sure audience understands why tooling is such an important thing.


### Boxen from Github

> Automate the pain out of your development environment. Boxen installs your dependencies so you can focus on getting things done.

[https://boxen.github.com](https://boxen.github.com)

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


### Perform following steps : Boostraping Steps

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
