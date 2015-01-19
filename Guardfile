# -*- mode: ruby -*-

guard :shell do
  watch(%r{^(src|tests)\/.*\/?[^./]+\.php$}) do |m|
    if system("php -l #{m[0]}")
      n "#{m[0]} is correct", 'PHP Syntax', :success
    else
      n "#{m[0]} is incorrect", 'PHP Syntax', :failed
    end
  end
end

if File.exists?(File.absolute_path('vendor/bin/phpunit'))
  guard :PHPUnit2, :tests_path => 'tests', :cli => '--colors --coverage-html ./dev/coverage', :all_after_pass => true, :command => './vendor/bin/phpunit' do
    watch(%r{^tests/.+Test\.php$})
    watch(%r{^src/(.+)\.php}) { |m| "tests/#{m[1]}Test.php" }
  end
end
