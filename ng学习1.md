### 1:@Injectable()

@Injectable()是ts的装饰器，当 TypeScript 看到@Injectable()装饰器时，就会记下本服务的元数据。 如果 Angular 需要往这个服务中注入其它依赖，就会使用这些元数据。

###2:*

星号表示作用于当前下的所有子元素


## 模板语法

1、插值方式：

        <p>{{msg}}</p>
        <p [innerHTML]="msg"></p>        
        
2、插入属性：

        <p data-mgs="msg"></p>
        <img bind-src="src" />
        <button [attr.aria-label]="actionName"></button>
        
3、绑定事件
    
        (事件名)="方法名(需要出入的参数...)"可用$event获得事件对象
        <p (click)="to($event)"></p>
        //备用形式
        <p on-click="to()"></p>
        
4、添加style
        
        //[ngstyle]可以用来设置多个样式，style在这里是一个对象
        <p [ngStyle]="style"></p>
        //根据isSpecial判断是red还是green
        <button [style.color]="isSpecial ? 'red': 'green'">Red</button>
        //属性需要单位时，还可以这样的带上单位
        <button [style.font-size.%]="!isSpecial ? 150 : 50" >Small</button>
        
5、添加class

        <p [Class]="class"></p>//这样会覆盖原有的class
        
        <div [class.special]="isSpecial">The class binding is special</div>
        //当isSpecial的求职结果为真时，将类special添加，反之移除。
        
        <div [ngClass]="currentClasses">This div is initially saveable, unchanged, and special</div>        
        this.currentClasses =  {
            saveable: this.canSave,
            modified: !this.isUnchanged,
            special:  this.isSpecial
          };
        ngClass绑定到一个 key:value 形式的控制对象。这个对象中的每个 key 都是一个 CSS 类名，如果它的 value 是true，这个类就会被加上，否则就会被移除。

6、双向绑定

Angular 以 NgModel 指令为桥梁，允许在表单元素上使用双向数据绑定。需要调用Input模块。

    import { Component, Input } from '@angular/core';
    @Input() msg: string = 'hello word';
    <input type="text" [(ngModel)]="msg" />
    
可以用以下方式模拟双向绑定

    <input type="text" [value]="msg" (input)="msg=$event.target.value" />
    
7、结构控制指令

NgIf

    <p *NgIf="isActive"></p>
    当isActive为真时将<p>插入dom，反之移除。
    
NgFor

    NgFor是一个重复指令，用来显示一组数据。
    <div *ngFor="let hero of heroes">{{hero.name}}</div>
    
    带索引的NgFor
    <div *ngFor="let hero of heroes; let i=index">{{i + 1}} - {{hero.name}}</div>