title: "外链播放页面url切换写法"
date: 2014-09-25 12:44:20
tags:
---

## from @fsk

# 外链播放页面url切换写法

    最近要写一个外链播放器，外链播放的url是：
    `</pre>

    1.[http://igame.163.com/#/outchain/0/17780022](http://igame.163.com/#/outchain/0/17780022).

    2.[http://igame.163.com/#/outchain/0/1778002/m/use](http://igame.163.com/#/outchain/0/1778002/m/use)

    3.[http://igame.163.com/#/outchain/0/1778002/m/how](http://igame.163.com/#/outchain/0/1778002/m/how)

    outchain后面的两个域对应外链的类型和id（专辑，单曲，歌单等），默认进去的是第2个url.在页面内需要实现一个tab切换的功能，对应的url条目便是2和3.

    ### java的配置配置代码

    <pre>`@Controller("webOutChainController")
    public class OutChainController extends BaseController{
        @RequestMapping(value = { "/outchain/{type}/{id}"}, method = { RequestMethod.GET })
        public ModelAndView myMusic(HttpServletRequest request,
                @PathVariable(value = "type") String skin,
                @PathVariable(value = "id") String id,
                ModelMap modelMap) {
            ...
            return new ModelAndView(getTemplate("web2/outchain/index"), modelMap);
        }
    }
    `</pre>

    /outchain/{type}/{id}指明了外链功能对应的url，实际页面对应的ftl路径在"web2/outchain/index"中进行指定。

    #### index.ftl中的配置代码：

*   [<span>使用插件</span>](outchain/${data.skin}/${data.id}#use)
*   [<span>插件使用流程</span>](outchain/${data.skin}/${data.id}#how)

    这里定义了两个tab切换标签，一个是“使用插件”，另外一个是“插件使用流程”。注意其中的li标签和a标签，里面的 class="z-slt"是当前选中标签后的附加样式，data-type = "use"负责和对应的url做匹配，后面的match方法要用到这个属性。a  href="outchain/${data.skin}/${data.id}#use"对应的是第一步跳转的url。

    下面是对应的js代码：

    <pre>`this.__tv = _t._$$TabView._$allocate({
    dataset:'type',
    selected:'z-slt',
    list:this.__nuseLis.getElementsByTagName('li')
    });

    _v._$addEvent(location,'urlchange',this.__onUrlChange._$bind(this));
    location.active();

    _pro.__onUrlChange = function(_event) {

        var _path = _event.path.replace("/","") || 'use';
        this.__tv._$match(_path);
        switch (_path) {
        case 'use':
            _e._$addClassName(this.__showDiv[1],"hide");
            _e._$delClassName(this.__showDiv[0],"hide");
        break;
        case 'how':
        _e._$addClassName(this.__showDiv[0],"hide");
        _e._$delClassName(this.__showDiv[1],"hide");
        break;
        }
    };

实际上，tabchange触发的事件是通过bom中的location进行触发控制的。nej里面的TabView控件只是负责显示内容的切换，this.__tv._$match(_path)也是负责拿当前的url和当前选中的tab项中的制定属性(本例中是dat-type)进行匹配，完成页面的切换逻辑。

这样做的一个好处就是，原来的url切换又主动的click形式变成了被动的访问形式，就是说，直接在url框里面敲[http://igame.163.com/#/outchain/0/1778002/m/how](http://igame.163.com/#/outchain/0/1778002/m/how)便可以访问到对应的tab节点，无需到特定的页面进行点击。