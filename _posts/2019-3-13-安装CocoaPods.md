# 安装CocoaPods

## 检查CocoaPods是否安装

```text
liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pod install --no-repo-update
-bash: pod: command not found
```

## 安装过程

1. 检查rvm是否安装。

    ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ rvm
    -bash: rvm: command not found
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ curl -L get.rvm.io | bash -s stable
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
    100   194  100   194    0     0    170      0  0:00:01  0:00:01 --:--:--   171
    100 24173  100 24173    0     0   9130      0  0:00:02  0:00:02 --:--:-- 18782
    Downloading https://github.com/rvm/rvm/archive/1.29.7.tar.gz
    Downloading https://github.com/rvm/rvm/releases/download/1.29.7/1.29.7.tar.gz.asc
    Found PGP signature at: 'https://github.com/rvm/rvm/releases/download/1.29.7/1.29.7.tar.gz.asc',
    but no GPG software exists to validate it, skipping.
    Installing RVM to /Users/liulongyang/.rvm/
        Adding rvm PATH line to /Users/liulongyang/.profile /Users/liulongyang/.mkshrc /Users/liulongyang/.bashrc /Users/liulongyang/.zshrc.
        Adding rvm loading line to /Users/liulongyang/.profile /Users/liulongyang/.bash_profile /Users/liulongyang/.zlogin.
    Installation of RVM in /Users/liulongyang/.rvm/ is almost complete:

      * To start using RVM you need to run `source /Users/liulongyang/.rvm/scripts/rvm`
        in all your open shell windows, in rare cases you need to reopen all shell windows.
    /Users/liulongyang/.bash_profile:5:export PATH=/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/liulongyang/Library/Android/SDK/platform-tools:/Users/liulongyang/Library/Android/SDK/tools

      * WARNING: Above files contains PATH= with no $PATH inside, this can break RVM,
        for details check https://github.com/rvm/rvm/issues/1351#issuecomment-10939525
        to avoid this warning prepend $PATH

    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ source /Users/liulongyang/.rvm/scripts/rvm
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ rvm -v
    rvm 1.29.7 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
    ```

2. 检查Ruby版本。Apple自带的需要升级。

    ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ rvm list known
    # MRI Rubies
    [ruby-]1.8.6[-p420]
    [ruby-]1.8.7[-head] # security released on head
    [ruby-]1.9.1[-p431]
    [ruby-]1.9.2[-p330]
    [ruby-]1.9.3[-p551]
    [ruby-]2.0.0[-p648]
    [ruby-]2.1[.10]
    [ruby-]2.2[.10]
    [ruby-]2.3[.8]
    [ruby-]2.4[.5]
    [ruby-]2.5[.3]
    [ruby-]2.6[.0]
    ruby-head

    # for forks use: rvm install ruby-head-<name> --url https://github.com/github/ruby.git --branch 2.2

    # JRuby
    jruby-1.6[.8]
    jruby-1.7[.27]
    jruby-9.1[.17.0]
    jruby[-9.2.5.0]
    jruby-head

    # Rubinius
    rbx-1[.4.3]
    rbx-2.3[.0]
    rbx-2.4[.1]
    rbx-2[.5.8]
    rbx-3[.100]
    rbx-head

    # TruffleRuby
    truffleruby[-1.0.0-rc10]

    # Opal
    opal

    # Minimalistic ruby implementation - ISO 30170:2012
    mruby-1.0.0
    mruby-1.1.0
    mruby-1.2.0
    mruby-1.3.0
    mruby-1[.4.1]
    mruby-2[.0.0]
    mruby[-head]

    # Ruby Enterprise Edition
    ree-1.8.6
    ree[-1.8.7][-2012.02]

    # Topaz
    topaz

    # MagLev
    maglev-1.0.0
    maglev-1.1[RC1]
    maglev[-1.2Alpha4]
    maglev-head

    # Mac OS X Snow Leopard Or Newer
    macruby-0.10
    macruby-0.11
    macruby[-0.12]
    macruby-nightly
    macruby-head

    # IronRuby
    ironruby[-1.1.3]
    ironruby-head
    ```

3. 升级Ruby版本。

   ```text
   liulongyangdeMacBook-Pro:ACTHelper liulongyang$ rvm install 2.4.5
    Searching for binary rubies, this might take some time.
    No binary rubies available for: osx/10.14/x86_64/ruby-2.4.5.
    Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
    Checking requirements for osx.
    Installing requirements for osx.
    Updating system..........
    Installing required packages: coreutils, libyaml, libksba, openssl@1.1.There were package installation errors, make sure to read the log.

    Try `brew tap --repair` and make sure `brew doctor` looks reasonable.

    Check Homebrew requirements https://docs.brew.sh/Installation
    ..
    Error running 'requirements_osx_brew_libs_install coreutils libyaml libksba openssl@1.1',
    please read /Users/liulongyang/.rvm/log/1552445539_ruby-2.4.5/package_install_coreutils_libyaml_libksba_openssl@1.1.log
    Requirements installation failed with status: 1.
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ ruby -v
    ruby 2.3.7p456 (2018-03-28 revision 63024) [universal.x86_64-darwin18]
   ```

4. 查看相关命令。

   ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ ruby --help
    Usage: ruby [switches] [--] [programfile] [arguments]
      -0[octal]       specify record separator (\0, if no argument)
      -a              autosplit mode with -n or -p (splits $_ into $F)
      -c              check syntax only
      -Cdirectory     cd to directory before executing your script
      -d, --debug     set debugging flags (set $DEBUG to true)
      -e 'command'    one line of script. Several -e's allowed. Omit [programfile]
      -Eex[:in], --encoding=ex[:in]
                      specify the default external and internal character encodings
      -Fpattern       split() pattern for autosplit (-a)
      -i[extension]   edit ARGV files in place (make backup if extension supplied)
      -Idirectory     specify $LOAD_PATH directory (may be used more than once)
      -l              enable line ending processing
      -n              assume 'while gets(); ... end' loop around your script
      -p              assume loop like -n but print line also like sed
      -rlibrary       require the library before executing your script
      -s              enable some switch parsing for switches after script name
      -S              look for the script using PATH environment variable
      -T[level=1]     turn on tainting checks
      -v, --verbose   print version number, then turn on verbose mode
      -w              turn warnings on for your script
      -W[level=2]     set warning level; 0=silence, 1=medium, 2=verbose
      -x[directory]   strip off text before #!ruby line and perhaps cd to directory
      --copyright     print the copyright
      --enable=feature[,...], --disable=feature[,...]
                      enable or disable features
      --external-encoding=encoding, --internal-encoding=encoding
                      specify the default external or internal character encoding
      --version       print the version
      --help          show this message, -h for short message
    Features:
      gems            rubygems (default: enabled)
      did_you_mean    did_you_mean (default: enabled)
      rubyopt         RUBYOPT environment variable (default: enabled)
      frozen-string-literal
                      freeze all string literals (default: disabled)
   ```

5. 查看gem版本并更新系统Ruby版本。

    ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ sudo gem -v
    Password:
    2.5.2.3
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ gem update --system
    Updating rubygems-update
    Fetching: rubygems-update-3.0.3.gem (100%)
    ERROR:  While executing gem ... (Gem::FilePermissionError)
        You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ sudo gem -v
    2.5.2.3
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ gem source -l
    *** CURRENT SOURCES ***

    https://rubygems.org/
    ```

6. 安装CocoaPods

   ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ sudo gem install -n /usr/local/bin cocoapods
    Fetching: i18n-0.9.5.gem (100%)
    Successfully installed i18n-0.9.5
    Fetching: activesupport-4.2.11.gem (100%)
    Successfully installed activesupport-4.2.11
    Fetching: nap-1.1.0.gem (100%)
    Successfully installed nap-1.1.0
    Fetching: fuzzy_match-2.0.4.gem (100%)
    Successfully installed fuzzy_match-2.0.4
    Fetching: cocoapods-core-1.6.1.gem (100%)
    Successfully installed cocoapods-core-1.6.1
    Fetching: claide-1.0.2.gem (100%)
    Successfully installed claide-1.0.2
    Fetching: cocoapods-deintegrate-1.0.3.gem (100%)
    Successfully installed cocoapods-deintegrate-1.0.3
    Fetching: cocoapods-downloader-1.2.2.gem (100%)
    Successfully installed cocoapods-downloader-1.2.2
    Fetching: cocoapods-plugins-1.0.0.gem (100%)
    Successfully installed cocoapods-plugins-1.0.0
    Fetching: cocoapods-search-1.0.0.gem (100%)
    Successfully installed cocoapods-search-1.0.0
    Fetching: cocoapods-stats-1.1.0.gem (100%)
    Successfully installed cocoapods-stats-1.1.0
    Fetching: netrc-0.11.0.gem (100%)
    Successfully installed netrc-0.11.0
    Fetching: cocoapods-trunk-1.3.1.gem (100%)
    Successfully installed cocoapods-trunk-1.3.1
    Fetching: cocoapods-try-1.1.0.gem (100%)
    Successfully installed cocoapods-try-1.1.0
    Fetching: molinillo-0.6.6.gem (100%)
    Successfully installed molinillo-0.6.6
    Fetching: atomos-0.1.3.gem (100%)
    Successfully installed atomos-0.1.3
    Fetching: CFPropertyList-3.0.0.gem (100%)
    Successfully installed CFPropertyList-3.0.0
    Fetching: colored2-3.1.2.gem (100%)
    Successfully installed colored2-3.1.2
    Fetching: nanaimo-0.2.6.gem (100%)
    Successfully installed nanaimo-0.2.6
    Fetching: xcodeproj-1.8.1.gem (100%)
    Successfully installed xcodeproj-1.8.1
    Fetching: escape-0.0.4.gem (100%)
    Successfully installed escape-0.0.4
    Fetching: fourflusher-2.2.0.gem (100%)
    Successfully installed fourflusher-2.2.0
    Fetching: gh_inspector-1.1.3.gem (100%)
    Successfully installed gh_inspector-1.1.3
    Fetching: ruby-macho-1.4.0.gem (100%)
    Successfully installed ruby-macho-1.4.0
    Fetching: cocoapods-1.6.1.gem (100%)
    Successfully installed cocoapods-1.6.1
    Parsing documentation for i18n-0.9.5
    Installing ri documentation for i18n-0.9.5
    Parsing documentation for activesupport-4.2.11
    Installing ri documentation for activesupport-4.2.11
    Parsing documentation for nap-1.1.0
    Installing ri documentation for nap-1.1.0
    Parsing documentation for fuzzy_match-2.0.4
    Installing ri documentation for fuzzy_match-2.0.4
    Parsing documentation for cocoapods-core-1.6.1
    Installing ri documentation for cocoapods-core-1.6.1
    Parsing documentation for claide-1.0.2
    Installing ri documentation for claide-1.0.2
    Parsing documentation for cocoapods-deintegrate-1.0.3
    Installing ri documentation for cocoapods-deintegrate-1.0.3
    Parsing documentation for cocoapods-downloader-1.2.2
    Installing ri documentation for cocoapods-downloader-1.2.2
    Parsing documentation for cocoapods-plugins-1.0.0
    Installing ri documentation for cocoapods-plugins-1.0.0
    Parsing documentation for cocoapods-search-1.0.0
    Installing ri documentation for cocoapods-search-1.0.0
    Parsing documentation for cocoapods-stats-1.1.0
    Installing ri documentation for cocoapods-stats-1.1.0
    Parsing documentation for netrc-0.11.0
    Installing ri documentation for netrc-0.11.0
    Parsing documentation for cocoapods-trunk-1.3.1
    Installing ri documentation for cocoapods-trunk-1.3.1
    Parsing documentation for cocoapods-try-1.1.0
    Installing ri documentation for cocoapods-try-1.1.0
    Parsing documentation for molinillo-0.6.6
    Installing ri documentation for molinillo-0.6.6
    Parsing documentation for atomos-0.1.3
    Installing ri documentation for atomos-0.1.3
    Parsing documentation for CFPropertyList-3.0.0
    Installing ri documentation for CFPropertyList-3.0.0
    Parsing documentation for colored2-3.1.2
    Installing ri documentation for colored2-3.1.2
    Parsing documentation for nanaimo-0.2.6
    Installing ri documentation for nanaimo-0.2.6
    Parsing documentation for xcodeproj-1.8.1
    Installing ri documentation for xcodeproj-1.8.1
    Parsing documentation for escape-0.0.4
    Installing ri documentation for escape-0.0.4
    Parsing documentation for fourflusher-2.2.0
    Installing ri documentation for fourflusher-2.2.0
    Parsing documentation for gh_inspector-1.1.3
    Installing ri documentation for gh_inspector-1.1.3
    Parsing documentation for ruby-macho-1.4.0
    Installing ri documentation for ruby-macho-1.4.0
    Parsing documentation for cocoapods-1.6.1
    Installing ri documentation for cocoapods-1.6.1
    Done installing documentation for i18n, activesupport, nap, fuzzy_match, cocoapods-core, claide, cocoapods-deintegrate, cocoapods-downloader, cocoapods-plugins, cocoapods-search, cocoapods-stats, netrc, cocoapods-trunk, cocoapods-try, molinillo, atomos, CFPropertyList, colored2, nanaimo, xcodeproj, escape, fourflusher, gh_inspector, ruby-macho, cocoapods after 11 seconds
    25 gems installed

   ```

7. 查看CocoaPods版本

   ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pod --version
    1.6.1
   ```

8. 创建podfile并安装相关第三方框架

    ```text
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pwd
    /Users/liulongyang/Documents/ACTHelper
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pod install --no-repo-update
    [!] No `Podfile' found in the project directory.
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ vim Podfile
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pod install --no-repo-update
    Analyzing dependencies
    Setting up CocoaPods master repo
      $ /usr/bin/git clone https://github.com/CocoaPods/Specs.git master --progress
      Cloning into 'master'...
      remote: Enumerating objects: 388, done.        
      remote: Counting objects: 100% (388/388), done.        
      remote: Compressing objects: 100% (263/263), done.        
      error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
      fatal: The remote end hung up unexpectedly
      fatal: early EOF
      fatal: index-pack failed
    [!] Unable to add a source with url `https://github.com/CocoaPods/Specs.git` named `master`.
    You can try adding it manually in `/Users/liulongyang/.cocoapods/repos` or via `pod repo add`.
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ pod install --no-repo-update
    Analyzing dependencies
    Setting up CocoaPods master repo
      $ /usr/bin/git clone https://github.com/CocoaPods/Specs.git master --progress
      Cloning into 'master'...
      remote: Enumerating objects: 129, done.        
      remote: Counting objects: 100% (129/129), done.        
      remote: Compressing objects: 100% (106/106), done.        
      remote: Total 2887097 (delta 36), reused 57 (delta 19), pack-reused 2886968        
      Receiving objects: 100% (2887097/2887097), 620.79 MiB | 685.00 KiB/s, done.
      Resolving deltas: 100% (1726815/1726815), done.
      Checking out files: 100% (311346/311346), done.

    CocoaPods 1.7.0.beta.2 is available.
    To update use: `sudo gem install cocoapods --pre`
    [!] This is a test version we'd love you to try.

    For more information, see https://blog.cocoapods.org and the CHANGELOG for this version at https://github.com/CocoaPods/CocoaPods/releases/tag/1.7.0.beta.2

    Setup completed
    Downloading dependencies
    Installing Alamofire (4.8.1)
    Installing HappyDNS (0.3.15)
    Installing PKHUD (5.2.1)
    Installing Qiniu (7.2.5)
    Installing Toaster (2.1.1)
    Generating Pods project
    Integrating client project

    [!] Please close any current Xcode sessions and use `ACTHelper.xcworkspace` for this project from now on.
    Sending stats
    Pod installation complete! There are 4 dependencies from the Podfile and 5 total pods installed.
    liulongyangdeMacBook-Pro:ACTHelper liulongyang$ 

    ```
