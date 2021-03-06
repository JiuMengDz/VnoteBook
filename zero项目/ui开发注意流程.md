# 1. ui开发注意流程

需要遵守相关的命名规范 这一部分需要快点熟悉起来

无请求返回的协议，需要在network中注册就可以反复监听，参考AchievementManager的reg_notify函数
有请求的协议监听可通过call的方式调用然后直接返回相应的回调，数据存储独立进行

## 1.1. 一些功能的实现过程
### 1.1.1. 功能跳转
![](_v_images/20200227093928279_5118.png =255x)
如果要实现这一的跳转，首先在J界面.xls中添加相应的跳转配置
随后使用`JumpUIManager.register(ui_name, on_jump_ui)`将相应的功能注册在跳转管理器中,注册的名字对应xls表中的名字

### 1.1.2. 主界面打开功能界面
**以背包界面的开启过程为例**
1. 在`win_main.lua`文件中的`after_ctor()`方法添加对应界面的回调绑定
2. 在`FairyGUI`标记器中的动效以`show`命名,在打开界面时会触发
3. 通过编辑相应界面的`manager`对象来实现对应ui的打开功能,同时为了能够实现跳转请参考功能跳转相关介绍
4. `manager`需要在`game_manager.lua`中统一初始化操作

### 1.1.3. 列表功能/渲染器
1. GUI编辑器生成的代码会自动写好`self.com_name.itemRenderer`的相关内容
2. 编辑对应的渲染方法,如`ui_callback.com_name_ir`
#### 1.1.3.1. 渲染方法
1. 首先声明`make_list_helper`的初始化工具
2. 随后在渲染方法中调用,其中`ctrl`即相应的ctrl组件,`index`是对应的数据对象

```lua
function CtrlItemGet:after_ctor(owner, root_cmp)
    self.list_helper = make_list_helper(self, self.list_get, CtrlGetway)
end

ui_callback.list_get_ir = function(self, index, obj)
    local ctrl, data = self.list_helper.on_item_renderer(index, obj)
    ctrl:set_info(data)
end
```

**!! helper中相应的方法**
在ui_utility.lua文件中
```lua
local function make_list_helper(ui, cmp_list, ctrl_class, click_cb)
    local item_ui_ctrls = {}
    local item_data_list = false

    local helper = {}

    function helper.set_data_list(data_list) end

    function helper.on_item_renderer(index, obj) end

    function helper.resize_to_fit() end

    if click_cb then
        cmp_list.onClickItem:Add(function (context)
            local obj = context.data
            local item = item_ui_ctrls[obj]
            click_cb(item,obj)
        end)
    end
    return helper
end
```
1. `set_data_list()` 重新赋值list中的数据,会调用到相应的list的重新渲染功能
2. `on_item_renderer()` 对象渲染的定义,返回相应的`ctrl组件`以及对于的`数据`
3. `resize_to_fit()` 顾名思义,即调整列表表现


### 1.1.4. 标签功能/渲染器

# 2. 功能的实现原理
## 2.1. 红点功能
