<template>
  <div id="app">
    <header>
      <h1>vm-select</h1>
      <p>vue multiple-select components</p>
    </header>
    <div id="banner">
      <span id="logo"></span>
      <a href="https://github.com/collins401/vm-select" class="button fork"><strong>View On GitHub</strong></a>
    </div><!-- end banner -->

    <div class="wrapper">
      <nav>
        <ul>
          <li class="tag-h1 active"><a href="/#vm-select">vm-select</a></li>
          <li class="tag-h2"><a href="/#label-key">label key</a></li>
          <li class="tag-h2"><a href="/#search">search</a></li>
          <li class="tag-h2"><a href="/#multiple">multiple-select</a></li>
          <li class="tag-h2"><a href="/#disabled">disabled</a></li>
          <li class="tag-h2"><a href="/#customDisabled">customDisabled</a></li>
          <li class="tag-h2"><a href="/#customLabel">customLabel</a></li>
          <li class="tag-h3"><a href="/#strings">strings</a></li>
        </ul>
      </nav>
      <section style="height: auto;">
      <h2 id="vm-select">vm-select</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options1" v-model="selected1"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected1}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">单选</div>
            <p>基本用法 <code>:options</code>和 <code>v-model</code></p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options1" v-model="selected1" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options1: ['github', 'gitlab', 'gitbook', 'gitalk', 'gitchat', 'gitshow', 'gitcool'],
      selected1: ''
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="label-key">label labelKey</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" label="name" label-key="id" v-model="selected2"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected2}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">label labelKey</div>
            <p>当 :options 为数组对象[{}]，props参数<code>label</code>、<code>labelKey</code>为必填, <code>label</code>为显示值，<code>labelKey</code> 为 v-model 返回值</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options2" label="name" label-key="id" v-model="selected2" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options2: [
        {id: 1, name: 'github'},
        {id: 2, name: 'gitlab'},
        {id: 3, name: 'gitbook'},
        {id: 4, name: 'gitalk'},
        {id: 5, name: 'gitchat'},
        {id: 6, name: 'gitshow'},
        {id: 7, name: 'gitcool'}
      ],
      selected2: 2
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="search">search</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" search multiple label="name" labelKey="id" v-model="selected3"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected3}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">搜索</div>
            <p>props 参数<code>search</code>为 true</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options1" search v-model="selected1" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options1: ['github', 'gitlab', 'gitbook', 'gitalk', 'gitchat', 'gitshow', 'gitcool'],
      selected1: ''
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="multiple">multiple select</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" search multiple label="name" labelKey="id" v-model="selected3"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected3}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">多选</div>
            <p>多选时<code>v-model</code>必须为 Array 格式</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options2" multiple v-model="selected3" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options2: [
        {id: 1, name: 'github'},
        {id: 2, name: 'gitlab'},
        {id: 3, name: 'gitbook'},
        {id: 4, name: 'gitalk'},
        {id: 5, name: 'gitchat'},
        {id: 6, name: 'gitshow'},
        {id: 7, name: 'gitcool'}
      ],
      selected3: [2, 3]
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="disabled">disabled</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options1" disabled v-model="selected4"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected4}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">搜索</div>
            <p>props 参数<code>disabled</code>为 true时，为不可选状态</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options1" disabled v-model="selected4" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options1: ['github', 'gitlab', 'gitbook', 'gitalk', 'gitchat', 'gitshow', 'gitcool'],
      selected4: 'gitbook'
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="customDisabled">customDisabled （Function）</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" :custom-disabled="disabledItemFunc" label="name" labelKey="id" v-model="selected2"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected2}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">搜索</div>
            <p>通过自定义函数方式禁止下拉框中，符合条件的选项。Function() =>{...}</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options2" :custom-disabled="disabledItemFunc" label="name" labelKey="id" v-model="selected2" &gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options1: ['github', 'gitlab', 'gitbook', 'gitalk', 'gitchat', 'gitshow', 'gitcool'],
      selected2: 2
    }
  },
  methods: {
    disabledItemFunc ({id}) {
      return id > 5
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="customLabel">customLabel （Function）</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" :custom-label="disabledLabelFunc" label="name" labelKey="id" v-model="selected2"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected2}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">搜索</div>
            <p>通过自定义函数方式实现label文字或样式显示的多样性</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options2" :custom-label="disabledLabelFunc" label="name" labelKey="id" v-model="selected2"&gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options2: [
        {id: 1, name: 'github'},
        {id: 2, name: 'gitlab'},
        {id: 3, name: 'gitbook'},
        {id: 4, name: 'gitalk'},
        {id: 5, name: 'gitchat'},
        {id: 6, name: 'gitshow'},
        {id: 7, name: 'gitcool'}
      ],
      selected2: 2
    }
  },
  methods: {
    disabledLabelFunc ({name, id}) {
      return `${id}---${name}`
    }
  }
}
        </v-code>
          </div>
        </div>
        <h2 id="strings">strings</h2>
        <div class="demo">
          <div class="demo-show">
            <div class="demo-components">
              <div class="demo-vm">
                <vm-select :options="options2" :strings="langs" search multiple label="name" labelKey="id" v-model="selected3"></vm-select>
              </div>
            </div>
            <div class="demo-value">
              v-model: {{selected3}}
            </div>
          </div>
          <div class="demo-code">
            <div class="demo-title">多选</div>
            <p>组件文字的自定义</p>
                    <v-code>
&lt;template&gt;
 &lt;vm-select :options="options2" :strings="langs" search multiple label="name" labelKey="id" v-model="selected3"&gt;&lt;/vm-select&gt;
&lt;/template&gt;
&lt;script&gt;
...
export default {
  data () {
    return {
      options2: [
        {id: 1, name: 'github'},
        {id: 2, name: 'gitlab'},
        {id: 3, name: 'gitbook'},
        {id: 4, name: 'gitalk'},
        {id: 5, name: 'gitchat'},
        {id: 6, name: 'gitshow'},
        {id: 7, name: 'gitcool'}
      ],
      selected3: [2, 3],
      langs: {
        placeholder: 'Select an Option...',
        search: 'Type in to search...',
        countSelected: 'Selected {0} Options', // {0}作为参数吧，不可缺少
        empty: 'No Options found',
        actionAll: 'Select All',
        actionNone: 'Unselect All'
      }
    }
  }
}
        </v-code>
          </div>
        </div>
      </section>
       <footer>
          <p>Project maintained by <a href="https://github.com/collins401">collins401</a></p>
      </footer>
    </div>
  </div>
</template>
<script>
import vmSelect from './components/vm-select/'
import vCode from './components/vcode/'
export default {
  data () {
    return {
      options1: ['github', 'gitlab', 'gitbook', 'gitalk', 'gitchat', 'gitshow', 'gitcool'],
      options2: [
        { id: 1, name: 'github' },
        { id: 2, name: 'gitlab' },
        { id: 3, name: 'gitbook' },
        { id: 4, name: 'gitalk' },
        { id: 5, name: 'gitchat' },
        { id: 6, name: 'gitshow' },
        { id: 7, name: 'gitcool' }
      ],
      selected1: '',
      selected2: 2,
      selected3: [2, 3],
      selected4: 'gitbook',
      disabled: true,
      selected: ['3', '4', '5'],
      langs: {
        placeholder: 'Select an Option...',
        search: 'Type in to search...',
        countSelected: 'Selected {0} Options',
        empty: 'No Options found',
        actionAll: 'Select All',
        actionNone: 'Unselect All'
      }
    }
  },
  components: {
    vmSelect,
    vCode
  },
  methods: {
    disabledItemFunc ({ id }) {
      return id > 5
    },
    disabledLabelFunc ({ name, id }) {
      return `${id}---${name}`
    }
  }
}
</script>
<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #494949;
}
.demo {
  border: 1px solid #ddd;
  border-radius: 2px;
}
.demo-show {
  display: flex;
}
.demo-code {
  border-top: 1px solid #ddd;
  position: relative;
  padding: 10px 10px 0;
}
.demo-title {
  display: inline-block;
  background-color: #fff;
  padding: 0 10px;
  position: absolute;
  top: -12px;
  left: 20px;
  font-weight: bold;
}
.demo-components {
  padding: 20px 10px;
  flex: 1;
}
.demo-value {
  width: 200px;
  padding: 20px 10px;
  border-left: 1px solid #ddd;
  margin-left: 20px;
}
.pre-code {
  text-align: center;
  line-height: 35px;
  color: #4276b6;
  cursor: pointer;
}
.demo-vm {
  width: 320px;
}
.demo-code > p > code {
  background: #e2c0c0;
  color: #e42e2e;
  text-shadow: none;
}
</style>
