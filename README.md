# Jekyll-macOS-install
A summary of steps needed to successfully install Jekyll in 2021 on macOS. 

-----------

I thought that after spending a significant amount of time trying to install and use the Jekyll web utility that I would catalog the steps I had to take in order to help future users. The directions from [Jekyll Website](https://jekyllrb.com) seemed to have a few issues that needed solving with the macOS install, mainly dealing with permissions. Try this first:

~~~~~~
gem install bundler jekyll
~~~~~~
If it worked, congratulations. If not, read on. 

-----------
# RUBY

macOS comes native with [Ruby](https://www.ruby-lang.org/en/documentation/installation/), however your version is most likely not up to date. Jekyll requires one of the latest builds of Ruby, so updating it is the first task. 

Check Ruby verison:
~~~~~~
ruby -v
% ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [x86_64-darwin19]
~~~~~~
You should have version 3.0.0 if installing after this post is written. If not, update Ruby. You will need to install [Homebrew](https://brew.sh), which you should have already if you do any fun projects on macOS.
~~~~~
brew install ruby
~~~~~
Exit and restart Terminal, then check the version again and you should see the update. During my install, I was required to run the following command to give myself file permissions.
~~~~~
sudo chown -R $(whoami) /usr/local/share/man/man8
~~~~~
Ensure that the correct pathway is added to Ruby. Depending on which shell you use, type the first for zsh and second for bash. This is the same instruction as on the Jekyll [macOS](https://jekyllrb.com/docs/installation/macos/) page.
~~~~~
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc

echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
~~~~~
Restart Terminal. Run
~~~~~
which ruby
% /usr/local/opt/ruby/bin/ruby
~~~~~
and ensure the final line matches. If it does not match, try adding the above path again and then restart Terminal once again. It should work then.

# Command Line Tools

If you're using XCode and it's up to date, you'll likely alreayd have the proper command line tools installed. No harm in trying to update them though.
~~~~~
xcode-select --install
~~~~~

# gem Update

Make sure the [RubyGem](https://rubygems.org/gems) installer is updated by running:
~~~~~~
sudo gem update --system
~~~~~~
It took a few minutes to update everything for me. Start reminding yourself of how much you love open source software, and the grind of installing it. 


# Bundler / Jekyll

Now you need to install Bundler and Jekyll. Bundler allows you to create bundles and Jekyll is the main web utility to build the website you always wanted. 
Running 
~~~~~~
sudo gem install bundler jekyll
~~~~~~

threw several errors during my install. One of which required me to change file permissions, and add a pathway for Ruby. From the official install guide, again, depending on your shell,
~~~~~~
echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc

echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile
~~~~~~
and replace 'X' with version. Again, 
~~~~~~
ruby -v
~~~~~~
will give you the correct values. I still had problems at this point installing Jekyll, however, Bundler installed fine. I ran this
~~~~~~
sudo gem update --system
~~~~~~
to update the gem system, followed by
~~~~~~
sudo gem install jekyll
~~~~~~
to finally install Jekyll. 
~~~~~~
jekyll -v
% jekyll 4.2.0
~~~~~~
Your version should be as new or newer than the above. 

# webrick
At this point you still won't be able to host your website locally. I had to install [webrick](https://rubygems.org/gems/webrick), an HTTP server toolkit, in order to host. 
~~~~~~~
bundle add webrick
~~~~~~~

------------
# Create a website
Navigate to the folder you want to use to store local files for your website. 
~~~~~~
cd ~/PATHWAY
~~~~~~
Create a new website with 
~~~~~
jekyll new WEBSITENAME
~~~~~
and a folder with a few files will be created. Navigate into it's directory
~~~~
cd /WEBSITENAME
~~~~
and then run 
~~~~
bundle exec jekyll serve
~~~~
to locally host the website. Output should include something like 
~~~~
Configuration file: ~/WEBSITENAME/_config.yml
            Source: /WEBSITENAME
       Destination: ~/WEBSITENAME/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.499 seconds.
 Auto-regeneration: enabled for '~/WEBSITENAME'
    Server address: http://XXX.X.X.X:4000/
  Server running... press ctrl-c to stop.
~~~~

# Navigating to your website
Simply go into your web browser and put in whats's after the server address field. You'll see something like [this](). Congratulations! Now comes the task of making your website interesting.

![](https://user-images.githubusercontent.com/57548527/110232588-7325fa00-7ed3-11eb-89c4-84ec0d9e266e.png)
