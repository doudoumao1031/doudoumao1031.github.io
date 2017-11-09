## Quick-start ##

	# Install Jekyll and Bundler gems through RubyGems
	gem install jekyll bundler
	
	# Create a new Jekyll site at ./myblog
	jekyll new myblog
	
	# Change into your new directory
	cd myblog
	
	# Build the site on the preview server
	bundle exec jekyll serve
	
	# Now browse to http://localhost:4000

**About Bundler**

- bundler is a gem that manages other Ruby gems. It makes sure your gems and gem versions are compatible, and that you have all necessary dependencies each gem requires.
- The Gemfile and Gemfile.lock files inform Bundler about the gem requirements in your site. If your site doesn’t have these Gemfiles, you can omit bundle exec and just run jekyll serve.
- When you run bundle exec jekyll serve, Bundler uses the gems and versions as specified in Gemfile.lock to ensure your Jekyll site builds with no compatibility or dependency conflicts.

一句话Bundler是依赖管理工具，通过Gemfile/Gemfile.lock配置