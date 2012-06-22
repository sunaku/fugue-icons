require 'rake/clean'

icons_src = FileList['src/*.psd']
Dir['icons*/', 'bonus/**/'].each do |icons_dir|
  css_file = icons_dir.sub(/\/$/, '.css')
  icons = FileList[icons_dir + '*.{png,gif}']

  file css_file => icons_src + icons do
    unless icons.empty?
      File.open(css_file, 'w') do |css_body|
        icons.each do |icon|
          css_body.puts <<CSS_RULE
.fugue-icons-#{icon.pathmap '%n'} {
  background-image: url(#{icon.pathmap '%-1d/%f'}) !important;
  background-repeat: no-repeat;
}
CSS_RULE
        end
      end
      warn "#{icons.length}\t#{css_file}"
    end
  end

  task :default => css_file
  CLOBBER.include css_file
end
