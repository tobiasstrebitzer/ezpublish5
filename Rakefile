require 'pathname'

legacy_path = Pathname('ezpublish_legacy/').realpath
app_path = Pathname('ezpublish/').realpath

task :clearcache do
    system("cd #{legacy_path} && php bin/php/ezcache.php --purge --clear-all")
    system("php ezpublish/console cache:clear")
end

task :cc do
    Rake.application.invoke_task("clearcache")
end

task :generateautoloads do
    system("cd #{legacy_path} && bin/php/ezpgenerateautoloads.php -o")
    system("cd #{legacy_path} && bin/php/ezpgenerateautoloads.php")
end

task :reconfigure do
    system("php ezpublish/console ezpublish:configure --env=prod ezdemo ezdemo_site_admin")
end

task :installassets do
    system("php ezpublish/console assets:install --symlink web/")
    system("php ezpublish/console ezpublish:legacy:assets_install --symlink web")
end

task :ezmagic do
    Rake.application.invoke_task("reconfigure")
    Rake.application.invoke_task("generateautoloads")
    Rake.application.invoke_task("installassets")
    Rake.application.invoke_task("cc")
end
