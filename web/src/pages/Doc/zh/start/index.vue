<template>
  <div>
    <h1>开始</h1>
<h2>安装</h2>
<pre class="hljs"><code>npm i simple-mind-map
</code></pre>
<p><code>0.2.0</code>版本之前的注意事项：</p>
<blockquote>
<p>注意：本项目为源码直接发布，并未进行打包，如果出现编译失败的情况，Vue CLI创建的项目可以在vue.config.js文件中增加如下配置来让babel-loader编译本依赖：</p>
<pre class="hljs"><code><span class="hljs-built_in">module</span>.exports = {
     <span class="hljs-attr">transpileDependencies</span>: [<span class="hljs-string">&#x27;simple-mind-map&#x27;</span>]
}
</code></pre>
<p>其他项目请自行修改打包配置。</p>
</blockquote>
<h2>使用</h2>
<blockquote>
<p>本仓库的<code>web</code>目录提供了一个基于<code>Vue2</code>的完整项目，如果你遇到了一些使用上的疑惑，可以参考该项目的实现。</p>
</blockquote>
<blockquote>
<p>想要了解在其他框架中的使用，你可以参考以下这些非官方的实现：</p>
<p>1.<a href="https://github.com/huangyuanyin/hyy-vue3-mindMap">https://github.com/huangyuanyin/hyy-vue3-mindMap</a>：一个基于 Vue3.2 +ElementPlus的思维导图。</p>
</blockquote>
<p>首先提供一个宽高不为0的容器元素：</p>
<pre class="hljs"><code><span class="hljs-tag">&lt;<span class="hljs-name">div</span> <span class="hljs-attr">id</span>=<span class="hljs-string">&quot;mindMapContainer&quot;</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span>&gt;</span>
</code></pre>
<p>另外再设置一下<code>css</code>样式：</p>
<pre class="hljs"><code><span class="hljs-selector-id">#mindMapContainer</span> * {
  <span class="hljs-attribute">margin</span>: <span class="hljs-number">0</span>;
  <span class="hljs-attribute">padding</span>: <span class="hljs-number">0</span>;
}
</code></pre>
<p>然后引入<code>simple-mind-map</code>库，创建一个实例：</p>
<pre class="hljs"><code><span class="hljs-keyword">import</span> MindMap <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;simple-mind-map&quot;</span>;

<span class="hljs-keyword">const</span> mindMap = <span class="hljs-keyword">new</span> MindMap({
  <span class="hljs-attr">el</span>: <span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">&#x27;mindMapContainer&#x27;</span>),
  <span class="hljs-attr">data</span>: {
    <span class="hljs-string">&quot;data&quot;</span>: {
        <span class="hljs-string">&quot;text&quot;</span>: <span class="hljs-string">&quot;根节点&quot;</span>
    },
    <span class="hljs-string">&quot;children&quot;</span>: []
  }
});
</code></pre>
<p>这样即可得一个思维导图。</p>
<p>如果你想要实现一个完整思维导图，那么通常你需要开发一些ui界面，通过<code>simple-mind-map</code>库提供的接口来实现更多功能。</p>
<p><code>simple-mind-map</code>支持丰富的配置、事件、命令，以及一些额外的插件扩展，阅读后续的文档来了解更多吧。</p>
<p>默认引入的是未打包的<code>ES</code>模块，且只包含核心功能，不包含未注册的插件内容，能有效减小体积，不过你需要在你的项目中配置<code>babel</code>编译<code>simple-mind-map</code>，防止一些较新的<code>js</code>语法部分浏览器不支持。</p>
<p>如果你不想一开始就加载所有插件，想在实例化了之后再异步加载和注册插件，可以这么做：</p>
<pre class="hljs"><code><span class="hljs-keyword">import</span>(<span class="hljs-string">&#x27;simple-mind-map/src/plugins/Export.js&#x27;</span>).then(<span class="hljs-function"><span class="hljs-params">res</span> =&gt;</span> {
  mindMap.addPlugin(res.default)
})
</code></pre>
<p>如果你需要<code>umd</code>模块格式的文件，比如以<code>CDN</code>的方式在浏览器上使用，那么你可以先通过npm安装<code>npm i simple-mind-map</code>，然后在<code>node_modules/simple-mind-map/dist/</code>目录中找到<code>simpleMindMap.umd.min.js</code>文件和<code>simpleMindMap.esm.min.css</code>文件，复制到你的项目中，然后在页面中引入：</p>
<pre class="hljs"><code><span class="hljs-tag">&lt;<span class="hljs-name">link</span> <span class="hljs-attr">rel</span>=<span class="hljs-string">&quot;stylesheet&quot;</span> <span class="hljs-attr">href</span>=<span class="hljs-string">&quot;simpleMindMap.esm.min.css&quot;</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">script</span> <span class="hljs-attr">scr</span>=<span class="hljs-string">&quot;simpleMindMap.umd.min.js&quot;</span>&gt;</span><span class="hljs-tag">&lt;/<span class="hljs-name">script</span>&gt;</span>
</code></pre>
<p>库会创建一个全局变量<code>window.simpleMindMap</code>，可以通过<code>window.simpleMindMap.default</code>获取到<code>MindMap</code>构造函数，然后正常实例化即可，详细信息可以把<code>window.simpleMindMap</code>打印出来看一下。</p>
<p>如果不方便使用<code>npm</code>来安装，也可以通过一些在线<code>CDN</code>服务来获取到这两个文件，比如：</p>
<pre class="hljs"><code>https://unpkg.com/simple-mind-map@0.10.2/dist/simpleMindMap.esm.css
https://unpkg.com/simple-mind-map@0.10.2/dist/simpleMindMap.umd.min.js
</code></pre>
<p>你可以替换其中的版本号。</p>
<p>这种方式的缺点是会包含所有的内容，包括你没有注册的插件（可以在这里<a href="https://github.com/wanglin2/mind-map/blob/main/simple-mind-map/full.js#L36">full.js</a>查看默认打包进文件的插件），所以整体体积会比较大，如果只想要打包指定的插件，你可以修改该文件，然后重新打包，如有需要也可以联系开发者。</p>
<p>（v0.5.4+）如果你想直接在浏览器端通过<code>ES</code>模块的方式来使用，你可以在<code>/simple-mind-map/dist/</code>目录中找到<code>simpleMindMap.esm.js</code>和<code>simpleMindMap.esm.css</code>文件。</p>
<p>也可以使用在线cdn服务，比如：</p>
<pre class="hljs"><code>https://unpkg.com/browse/simple-mind-map@0.9.2/dist/
</code></pre>
<p>可以找到某个版本的所有打包后的文件。</p>
<h2>开发</h2>
<p>如果你只是使用库的话可以不用阅读此小节。</p>
<h3>本地开发</h3>
<pre class="hljs"><code>git <span class="hljs-built_in">clone</span> https://github.com/wanglin2/mind-map.git
<span class="hljs-built_in">cd</span> mind-map
<span class="hljs-built_in">cd</span> simple-mind-map
npm i
npm link
<span class="hljs-built_in">cd</span> ..
<span class="hljs-built_in">cd</span> web
npm i
npm link simple-mind-map
npm run serve
</code></pre>
<blockquote>
<p>如果安装依赖出错，可以尝试调整node版本，作者使用的是14.x版本。</p>
</blockquote>
<h3>打包库</h3>
<p>自<code>0.2.0</code>版本开始增加了对核心库<code>simple-mind-map</code>的打包，复用了示例项目<code>web</code>的打包工具。</p>
<pre class="hljs"><code><span class="hljs-built_in">cd</span> web
npm run buildLibrary
</code></pre>
<p>打包入口为<code>simple-mind-map/full.js</code>，默认会引入所有插件，如果你不需要所有插件的话，那么可以修改该文件，只引入你需要的插件，这样可以减少打包后的文件体积。</p>
<p><code>simple-mind-map</code>库的<code>package.json</code>文件提供了两个导出字段：</p>
<pre class="hljs"><code>{
  <span class="hljs-attr">&quot;module&quot;</span>: <span class="hljs-string">&quot;index.js&quot;</span>,
  <span class="hljs-attr">&quot;main&quot;</span>: <span class="hljs-string">&quot;./dist/simpleMindMap.umd.min.js&quot;</span>,
}
</code></pre>
<p>支持<code>module</code>字段的环境会以<code>index.js</code>为入口，否则会以打包后的<code>simpleMindMap.umd.min.js</code>为入口。</p>
<h4>生成TypeScript类型文件</h4>
<pre class="hljs"><code><span class="hljs-built_in">cd</span> simple-mind-map
npm run types
</code></pre>
<p>即可得到<code>simple-mind-map/types/</code>目录下的类型文件。</p>
<h3>编译文档</h3>
<pre class="hljs"><code><span class="hljs-built_in">cd</span> web 
npm run buildDoc
</code></pre>
<h3>打包demo</h3>
<pre class="hljs"><code><span class="hljs-built_in">cd</span> web
npm run build
</code></pre>
<p>会自动把<code>index.html</code>移动到根目录。</p>
<h2>问题</h2>
<h3>1.在Vite中使用报错，提示xml-js依赖出错</h3>
<p>解决方法：使用如下引入方式：</p>
<pre class="hljs"><code><span class="hljs-keyword">import</span> MindMap <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;simple-mind-map/dist/simpleMindMap.umd.min&quot;</span>
</code></pre>
<p><code>simple-mind-map</code>包提供未打包的入口字段<code>module</code>，依赖的<code>xml-js</code>包需要引入<code>node</code>环境下的包，所以在<code>Vite</code>中获取不到会报错，所以指定引入打包后的入口，相关包都已打包进产物，所以不会报错。</p>
<p>如果需要二次开发，也就是必须要使用未打包代码的话，如果你不需要解析<code>xmind</code>文件的话，可以去除<code>xmind</code>模块，如果需要的话那么可以尝试换成其他的解析<code>xml</code>为<code>json</code>的库。</p>
<h3>2.报错<code>Getting bbox of element &quot;text&quot; is not possible: TypeError: Cannot read properties of undefined (reading 'apply')</code></h3>
<p>原因为安装的<code>@svgdotjs/svg.js</code>版本太高，手动降到<code>3.0.16</code>版本即可。</p>
<h3>3.TypeError: Cannot read properties of undefined (reading 'prototype') at sax.js:222:46</h3>
<p>可以在打包配置文件中增加如下配置：</p>
<pre class="hljs"><code>resolve: { <span class="hljs-attr">alias</span>: { <span class="hljs-attr">stream</span>: <span class="hljs-string">&quot;stream-browserify&quot;</span> } }
</code></pre>
<p>不同的打包工具可能具体配置不一样，原理就是排除<code>stream</code>依赖。</p>
<h3>4.点击【新建】、【打开】、【另存为】按钮时提示浏览器不支持，或者非https协议。</h3>
<p>浏览器上操作电脑本地文件使用的是<a href="https://developer.mozilla.org/zh-CN/docs/Web/API/Window/showOpenFilePicker">window.showOpenFilePicker</a>api，如果不支持，要么是浏览器不支持这个API，要么是因为页面非https协议，你可以按F12，或者在页面通过鼠标右键菜单中的【检查】打开浏览器控制台，在其中的【控制台】或【console】tab中输入<code>window.showOpenFilePicker</code>按回车，如果返回<code>undefined</code>则代表不支持，如果返回的不是这个，而页面依旧提示提示浏览器不支持，或者非https协议，那么可以提交issue，或者联系作者。</p>
<h3>5.引入simple-mind-map报错，报错信息如下：</h3>
<img src="../../../../assets/img/docs/错误.jpg" style="width: 850px" />
<p>这是因为你的构建环境不支持该js语法，该语法出自<code>@svgdotjs/svg.js</code>库，解决方法如下：</p>
<p>1.手动降低<code>@svgdotjs/svg.js</code>库的版本，你可以在你的项目中手动安装低版本，比如：<code>npm i @svgdotjs/svg.js@3.2.0</code></p>
<p>2.不降低版本的话，可以通过修改你的构建工具的相关配置，修改<code>babel</code>的配置，让它编译一下<code>node_modules</code>中的<code>simple-mind-map</code>库，或<code>@svgdotjs/svg.js</code>库，如果用的是<code>vue-cli</code>或<code>vite</code>，它们也直接提供了相关配置。另外需要安装编译该语法的<code>babel</code>插件，并且配置到<code>babel</code>的配置文件中：</p>
<p><code>@babel/plugin-proposal-nullish-coalescing-operator</code>、<code>@babel/plugin-proposal-optional-chaining</code>。</p>

  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>