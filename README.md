# tmap-echarts

Tmap-echarts是在[天地图](http://lbs.tianditu.gov.cn/api/js4.0/guide.html)4.0图层上展示echarts图表的插件，通过实现自定义覆盖物完成图表的渲染，几乎支持echarts中的所有图表，包括3D图表。

相比盖一个div在地图上，自定义覆盖物可以更灵活的去展示想要的效果，能与地图更完美的结合。

甚至可以在上面再盖一个echarts的百度地图（未尝试过）

# 效果

如果见过这个：https://echarts.apache.org/examples/zh/editor.html?c=map-usa-pie 那应该很好理解该插件。

![效果图](https://pic.imgdb.cn/item/6392ea3db1fccdcd369cee0d.gif)



# 安装

```
npm i tmap-echarts -S
```

# 在线示例

<iframe src="https://codesandbox.io/embed/tmap-echarts-demo-s71ieb?autoresize=1&fontsize=14&hidenavigation=1&theme=dark&view=preview"style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"title="tmap-echarts-demo"allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"></iframe>


[![Edit tmap-echarts-demo](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/tmap-echarts-demo-s71ieb?fontsize=14&hidenavigation=1&theme=dark&view=preview)



# 使用教程

```js
import("tmap-echarts").then(({ echartsOverlay }) => {
      const option = {
        tooltip: {
          trigger: "item",
        },
        series: [
          {
            name: "Access From",
            type: "pie",
            radius: "50%",
            data: [
              { value: 1048, name: "Search Engine" },
              { value: 735, name: "Direct" },
              { value: 580, name: "Email" },
              { value: 484, name: "Union Ads" },
              { value: 300, name: "Video Ads" },
            ],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)",
              },
            },
          },
        ],
      };
      const overlay = new echartsOverlay(
        new window.T.LngLat(116.40769, 39.89945),
        {
          width: 300,
          echartsOptions: option,
          updateCallBack: (chartView, map) => {
            // console.log(chartView, map);
            // console.log(map.getZoom());
            // console.log(chartView.getDom());
            // console.log(this);
          },
        }
      );
      map.addOverLay(overlay);
    });
```

## 更新数据

```js
// echarts的option
overlay.refreshEchartsOption(options)

// 或者获取echart视图
overlay.getChart().setOption(options)
```

## 获取echart视图

```js
overlay.getChart()
```

## 隐藏/显示

```js
// 隐藏
overlay.hide()
// 显示
overlay.show()
```

## 删除视图/销毁视图

```js
map.removeOverLay(overlay)
```

# 配置项

| 参数    | 说明                 | 类型   | 默认值 |
| ------- | -------------------- | ------ | ------ |
| lnglat  | 放置图表的经纬度位置 | lnglat | 无     |
| options | 配置对象             | object | {}     |

## options

| 参数           | 说明                                                         | 类型     | 默认值 |
| -------------- | ------------------------------------------------------------ | -------- | ------ |
| echartsOptions | echarts图表的option                                          | object   | {}     |
| width          | 容器的长                                                     | Number   | 200    |
| Height         | 容器的高                                                     | Number   | 200    |
| index          | 容器在地图中的层级                                           | Number   | 无     |
| isDisScale     | 是否禁用自动缩放                                             | Boolean  | false  |
| scaleNum       | 自动缩放的比例系数<br />计算方式为`(zoom / 10) * this.width * this.scaleNum` | Number   | 1      |
| updateCallBack | update的回调函数，返回参数（chartView, map）=> {}            | Function | Null   |

# 依赖

- [echarts](https://www.npmjs.com/package/echarts) 

- [echarts-gl](https://www.npmjs.com/package/echarts-gl)

# 其他

博客：[随机的布尔值](https://bingyishow.top/)

# 赞助

[赞助一杯咖啡](https://bingyishow.top/11.html)
