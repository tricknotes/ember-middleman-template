require 'thor/group'

module Middleman
  class Generator < ::Thor::Group
    include ::Thor::Actions

    class_option 'css_dir',
      default: 'stylesheets',
      desc:    'The path to the css files'

    class_option 'js_dir',
      default: 'javascripts',
      desc:    'The path to the javascript files'

    class_option 'images_dir',
      default: 'images',
      desc:    'The path to the image files'

    source_root File.join(File.expand_path(File.dirname(__FILE__)), 'templates')

    def build_scaffold
      template 'config.tt', File.join(location, 'config.rb')
      template 'Gemfile.tt', File.join(location, 'Gemfile')

      empty_directory File.join(location, 'source', options[:css_dir])
      empty_directory File.join(location, 'source', options[:images_dir])

      js_dir = File.join(location, 'source', options[:js_dir])

      directory File.join('source', 'javascripts'), js_dir

      %w(
        initializers
        models
        controllers
        helpers
        views
        components
        templates
        routes
      ).each do |type|
        empty_directory File.join(js_dir, type)
        copy_file 'gitkeep', File.join(js_dir, type, '.gitkeep')
      end

      %w(
        source/layouts/layout.html.erb
        source/index.html.erb
        source/javascripts/templates/index.js.hbs
      ).each do |file|
        copy_file file, File.join(location, file)
      end
    end

    private

    def location
      '.'
    end
  end
end
