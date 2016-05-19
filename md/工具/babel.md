# babel的使用

##1. babel的介绍
1. <a href="http://babeljs.io/" style="color:red">babel是什么</a>
2. babel是javascript的编译器，代码到代码的编译(es6/es7编译成es5)

##2. `babel`命令行的具体使用
1. 安装babel的终端 `npm install babel-cli --global`
2. 如果项目中使用建议安装在项目里面`npm install babel-cli --save-dev`
2. `babel src.js -o(--out-file) build.js` 把src.js文件编译到build.js文件里面
3. `babel src -d (--out-dir) build` 把src目录下面的所有的文件编译到build目录下面
4. 更多的命令通过`babel --help`查看

##3. 项目根目录新建`.babelrc`文件，里面放入配置文件
1. 预设presets是一些插件的组合，比如`babel-preset-2015`
2. 如果需要支持es6语法的话，先安装`npm install babel-preset-2015 --save-dev` 然后在`presets`添加`es2015`
3. plugins插件,babel6.0以上做了调整，bable都是通过plugin来编译代码的

<pre>
{
    "presets":["es2015","react"],
    "plugins": ["transform-es2015-arrow-functions"]
}
</pre>
##4. 在`package.json`里面的`scripts`里面配置运行脚本然后通过`npm run + 命令`去执行(可以节省代码的书写量)

<pre>
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "./node_modules/.bin/babel  src -wd build",
    "dev": "./node_modules/.bin/gulp"
  }
</pre>

##5. `babel`在项目里面一般不是单独去用的，因为项目里面还有`less`文件的编译，所以一般配合`gulp`或者`webpack`去使用
#### `babel+gulp`的使用
1. 需要在根目录下面新建gulpfile.js文件
2. `npm install gulp gulp-babel --save`安装gulp和gulp-babel
3. gulp-babel就是babel的核心代码，它会去根目录查找.babelrc配置文件,如果没有这个配置文件的话，我们在调用的时候就要传入相应的预设或者插件
4. 在package.json文件scripts里面配置`"dev:./node_modules/.bin/gulp"`,运行`npm run dev`

<pre>
var gulp = require('gulp');
var babel = require('gulp-babel');

gulp.task('babel', function(){
    gulp.src('src/*.js')
    .pipe(babel())
    .pipe(gulp.dest('build'))
})

gulp.task('default', ['babel']);
</pre>


