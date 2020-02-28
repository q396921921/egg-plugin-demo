# egg-plugin-demo
解释：通过plugin.Js中package引入，一般挂载在egg的app上
(2)注意1：如果我们的插件需要引入”xxx” npm包,那么我们就需要在package.json中配置我们强依赖的npm包名字。例如
"dependencies": {
    "moment": "^2.24.0"
  },
或者直接通过npm i moment --production命令，直接引入该包。
(3)注意2，我们将自己写好的插件，如果需要什么强依赖的包，需要提前通过npm i xxx --production，引入到项目里
①【因为在此种npm link模式下，他只会在我们插件自己的项目node_modules目录中寻找所依赖的包，而不是引入他的项目！！！！并且，此种模式下如果不在原插件中进行引入依赖，那么在引入他的项目中运行npm i 等安装依赖包的命令，就会自动将该依赖删除。需要我们重新在引用插件的项目中运行npm link 插件项目名(并且依赖仍是未安装的)】
②
然后再通过在插件项目中根目录下运行npm link命令。生成一个快捷方式。
再然后在引入插件项目根目录下运行npm link 插件项目名  命令。然后通过plugin.js文件中
exports.xxx = {
  enable: true,
  package: 'egg-test3',
}
xxx没什么实际意义，就是为了便于区分我们引入的包，随意定义名字都可以。Package必须与egg插件package.json中的name一样，并且name必须是以egg-开头的名字【egg插件命名规则请参考官方：https://eggjs.org/zh-cn/advanced/plugin.html#%E6%8F%92%E4%BB%B6%E8%A7%84%E8%8C%83 】