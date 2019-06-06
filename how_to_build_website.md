## jekyll + github page
In windows:
1. Download and install ruby: [rubyinstaller-2.6.3-1-x86.exe](https://github.com/oneclick/rubyinstaller2/releases)
2. check whether installation successed. `$ ruby -v`, `$gem -v`.
3. install [jekyll](http://jekyllcn.com/): `$ gem install jekyll`.
4. install bundle: `$ gem install bundler`
5. install jekyll-paginate: `$ gem install jekyll-paginate`
6. set up a new project: `$ jekyll new blog // blog is your project name`
7. start jekyll server: `$ cd ./blog`, `$ jekyll serve`. If failed, check which program has using 4000 port by `$ netstat -aon | findstr "4000"`, and stop the service of this program. [Please see](https://segmentfault.com/q/1010000010483290/a-1020000010487387)
8. open `http://localhost:4000` in your brower.

## Build up your new websize
1. git clone the project: `$git clone https://github.com/Huxpro/huxblog-boilerplate.git`
2. start jeky server: `$ cd huxblog-boilerplate`, `$ jekyll serve`.
8. open `http://localhost:4000` in your brower.
