# Bootstrap Notes

## 一、容器

- 流体容器
- 固定容器
  - 阈值
    - 大于等于1200(lg—大屏pc)			width：1170(1140+槽宽)
    - 992~1200(md—中屏pc)                   width：970(940+槽宽)
    - 768~992(sm—平板)                     width：750(720+槽宽)
    - 小于768(xs—移动手机)                      width：auto(相当于流体容器)
- 栅格系统

## 二、栅格源码分析

### 2.1 流体容器&固定容器 公共样式

- margin-right：auto
- margin-left：auto
- padding-left：15px

-  padding-right：15px

### 2.2 固定容器 特定样式

- 顺序不可变(从小到大)

```less
  @media (min-width: @screen-sm-min) {
    width: @container-sm;
  }
  @media (min-width: @screen-md-min) {
    width: @container-md;
  }
  @media (min-width: @screen-lg-min) {
    width: @container-lg;
  }
```

### 2.3 行

- margin-left： -15px;
- margin-right:    -15px;

### 2.4 列

```less
.make-grid-columns()---->
	.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1,
    .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2
    ...
    .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12{
        position: relative;
        min-height: 1px;
        padding-left:  ceil((@grid-gutter-width / 2));
        padding-right: floor((@grid-gutter-width / 2));
    }
```

```less
.make-grid(xs)--->
	float-grid-columns(@class);
	/*.col-xs-1,.col-xs-2,.col-xs-3,.col-xs-4,...,.col-xs-12{
	float:left;
	}
	*/
	.loop-grid-columns(@grid-columns, @class, width);
    /*
	.col-xs-12{
		width:12/12;
    }
	.col-xs-11{
		width:11/12;
    }
	...
	.col-xs-1{
		width:1/12;
    }
	*/
	.loop-grid-columns(@grid-columns, @class, pull);
  	.loop-grid-columns(@grid-columns, @class, push);
	/*
		push							pull
	col-xs-push-12{					col-xs-pull-12{
		left:12/12;						right:12/12;
	}								}
	.col-xs-push-11{
		left:11/12;
    }
	...								...
	.col-xs-push-1{
		left:1/12;
    }
    .col-xs-push-0{					.col-xs-pull-0{
        left:auto;						right:auto;
	}								}
	*/
  	.loop-grid-columns(@grid-columns, @class, offset);
	/*
	.col-xs-offset-12{
		margin-left:12/12;
    }
	.col-offset-xs-11{
		margin-left:11/12;
    }
	...
	.col-offset-xs-1{
		margin-left:1/12;
    }
    .col-offset-xs-0{
        margin-left:0;
    }
	*/
```

### 2.5 栅格盒模型的精妙之处

容器   两边具有15px的padding（padding-left  \  padding-right）

行       两边具有 -15px的margin

列    	两边具有15px的padding

- 为了维护槽宽的规则，列两边必须得有15px的padding
- 为了能使列嵌套行，行两边必须有 -15px的padding
- 为了让容器可以包裹住行，容器两边必须要有15px的padding