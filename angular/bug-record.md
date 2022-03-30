# *Angular BUG Record*

## use apex-chart in mat-tab, when change tab, chart has error, and has`t show when screen change size 

>By default, the tab contents are eagerly loaded. 
>Eagerly loaded tabs will initalize the child components but not inject them into the DOM until the tab is activated.

初始化时 mat-tab将所有子组件初始化，但并不会将其注入dom树。也就是说在在切换时才会将子组件注入，但是此时并不会触发子组件construct 和 ngOnInit 方法 但由于我chart Options的赋值写在construct中，所以切换时缺失options 引起报错 并且在改变屏幕时 chart报错不显示。
>解决办法：
>> 1.使用 **<ng-template matTabContent></template>** 懒加载，每次切换时重新渲染组件。
>> 2.如果每次重新渲染组件开销过大，考虑将chart options的赋值移出construct。直接复制在变量上。