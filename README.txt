有些时候文章中出现一些奇怪字符会造成发布失败，可以用 detect_code.cpp 来检查。

brew install 安装的 node 有问题，需要自己去 nodejs 官网下载 .pkg 格式的安装包安装。

重新安装的时候，git clone 下来，执行 npm install.



修改了 archive 的每页文章条数：
/Users/tangqiao/work/git/hexo/node_modules/hexo-generator-archive/index.js:
/Users/tangqiao/work/git/hexo/node_modules/hexo-generator-category/index.js
/Users/tangqiao/work/git/hexo/node_modules/hexo-generator-tag/index.js

广告位修改文章：
themes/jacman/layout/_widget/sponsor.ejs

# 初使化
npm install -g hexo-cli
cd <blog folder>
npm install

# 设置发布
git clone git@github.com:tangqiaoboy/tangqiaoboy.github.com.git public

# 设置皮肤
mkdir themes
cd themes
git clone git@github.com:tangqiaoboy/jacman.git

历史广告：

<a target="_blank" href="https://www.boxueio.com/register/30b8aaac334ecfa97fe6937cc091aca6">
  <img src="http://wx1.sinaimg.cn/large/65dc76a3ly1fduudtak0zj206j05kglq.jpg" width="235px" height="200px" />
  </a>
  <br /><br />