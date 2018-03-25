今天总结一下布局，之前校招面试的时候貌似很喜欢考布局，例如两栏自适应布局、三栏自适应布局等等，实现的方法多种多样，总结一下以后就不乱了。

两栏布局
----
这里我们讲的两栏布局一般是左定宽右自适应的
![图片描述][1]


 

 - **左float+右margin-left**
	
		html, body {
			height: 80%;
		}
		.wrapper {
			height: 100%;

		}
		.common {
			height: 100%;
		}
		.aside {
			width: 200px;
			background: green;
			float: left;
		}
		.main {
			background: red;
			margin-left: 200px;
		}
        <div class="wrapper">
		    <div class="aside common">
			    <h2>侧栏</h2>
		    </div>
		    <div class="main common">
			    <h1>主栏</h1>
		    </div>
	    </div>
	    

 - **双float+右calc**
        html, body {
			height: 80%;
		}
		.wrapper {
			height: 100%;

		}
		.common {
			height: 100%;
			float: left;
		}
		.aside {
			width: 200px;
			background: green;
		}
		.main {
			background: red;
			width: calc(100% - 200px);
		}
        <div class="wrapper">
		    <div class="aside common">
			    <h2>侧栏</h2>
	    	</div>
		    <div class="main common">
			    <h1>主栏</h1>
    		</div>
	    </div>
	    
	 

 -  **左absolute+右margin-left**
		html, body {
			height: 80%;
		}
		.wrapper {
			height: 100%;
			position: relative;
		}
		.common {
			height: 100%;
		}
		.aside {
			position: absolute;
			left: 0px;
			width: 200px;
			background: green;
		}
		.main {
			background: red;
			margin-left: 200px;
		}
       	<div class="wrapper">
       		<div class="aside common">
		    	<h2>侧栏</h2>
	    	</div>
    		<div class="main common">
		    	<h1>主栏</h1>
	    	</div>
    	</div>

   

 - **双absolute**
		.wrapper {
			height: 100%;
			position: relative;
		}
		.common {
			height: 100%;
		}
		.aside {
			background: green;
			position: absolute;
			left: 0px;
			width: 200px;
		}
		.main {
			background: red;
			position: absolute;
			left: 200px;
			right: 0px;
		}
       	<div class="wrapper">
		    <div class="aside common">
			    <h2>侧栏</h2>
    		</div>
	    	<div class="main common">
		    	<h1>主栏</h1>
    		</div>
	    </div>
 - **flex**
		html, body {
			height: 80%;
		}
		.wrapper {
			height: 100%;
			display: flex;
		}
		.common {
			height: 100%;
		}
		.aside {
			flex: 0 1 200px;
			background: green;
		}
		.main {
			flex-grow: 1;
			background: red;
		}
        <div class="wrapper">
		    <div class="aside common">
			    <h2>侧栏</h2>
    		</div>
	    	<div class="main common">
		    	<h1>主栏</h1>
    		</div>
	    </div>

三栏布局
----
这里说的三栏布局是左右定宽，中间自适应
![图片描述][2]


  [1]: /img/bV6N2P
  [2]: /img/bV6Oaj

 - **float left + margin-left/margin-right + float right**
		html, body {
			height: 100%;
		}
		.wrapper {
			height: 100%;
		}
		.left {
			height: 100%;
			width: 200px;
			float: left;
			background: green;
		}
		.right {
			height: 100%;
			width: 200px;
			float: right;
			background: blue;
		}
		.main {
			height: 100%;
			margin: 0px 200px;
			background: red;
		}
        <div class="wrapper">
    		<div class="left"></div>
    		<div class="right"></div>
    		<div class="main"></div>
	    </div>
 - BFC特性的三栏布局（后面总结BFC）
    	.left {
		    float: left;
		    height: 200px;
		    width: 100px;
		    background-color: red;
		}
		.right {
		    width: 200px;
		    height: 200px;
		    float: right;
		    background-color: blue;
		}	
		.main {
		    height: 200px;
		    overflow: hidden;
		    background-color: green;
		}
        <div class="container">
            <div class="left">
        	    <h1>Left</h1>
            </div>
            <div class="right">
            	<h1>Right</h1>
            </div>
            <div class="main">
            	<h1>Content</h1>
            </div>
        </div>
        
 - **圣杯布局**
        html, body {
			height: 100%;
		}
		.wrapper {
			height: 80%;
			padding: 0px 200px;
		}
		.common {
			position: relative;
			float: left;
			height: 100%;
			color: white;
		}
		.content {
			background: red;
			width: 100%;
		}
		.left {
			background: blue;
			width: 200px;
			margin-left: -100%;
			left: -200px;
		}
		.right {
			background: green;
			width: 200px;
			margin-left: -200px;
			right: -200px;
		}
        <div class="wrapper">
    		<div class="content common">
	    		<h1>Content</h1>
		    </div>
    		<div class="left common">
	    		<h1>Left</h1>
		    </div>
    		<div class="right common">
	    		<h1>Right</h1>
		    </div>
    	</div>
    	
中间内容区content在最前面，后面依次是left和right。
首先Content、Left、Right都设为float:left，然后Content宽度设为100%，此时Left和Right被挤到了下面一行；
将Left的margin-left设为-100%，Left被拉到了Content的最左边，且遮挡了Content的左边部分；将Right的负外左边距设为它的宽度，Right被拉到了Content的最右边，且遮住了Content的右边部分
此时再设置wapper的左右padding分别为Left和Right的宽度，此时Content的宽度被压缩到了合适的位置，但是Left和Right仍没有到正确的位置
最后通过相对定位，设置Left和Right都为relative，且Left的left设为其负宽度，Right的right设为其负宽度
    
    
 - 双飞翼布局
		html, body {
			height: 100%;
		}
		.common {
			height: 100%;
			float: left;
			color: #fff;
		}
		.content {
			background: red;
			width: 100%;
		}
		.content-in {
			margin: 0px 200px;
		}
		.left {
			background: blue;
			width: 200px;
			margin-left: -100%;
		}
		.right {
			background: green;
			width: 200px;
			margin-left: -200px;
		}
        <div class="content common">
		    <div class="content-in">
			    <h1>Content</h1>
    		</div>
	    </div>
    	<div class="left common">
	    	<h1>Left</h1>
    	</div>
	    <div class="right common">
		    <h1>Right</h1>
    	</div>
首先Content、Left、Right都设置float:left；
将Left的margin-left设为-100%，Left被拉到了Content的最左边，且遮挡了Content的左边部分；将Right的负外左边距设为它的宽度，Right被拉到了Content的最右边，且遮住了Content的右边部分
Content-in设置左右margin分别为Left宽度和Right宽度即可
 - **绝对定位**
		.wrapper {
			height: 80%;
			position: relative;
		}
		.common {
			height: 100%;
			color: white;
		}
		.left {
			position: absolute;
			top: 0px;
			left: 0px;
			width: 200px;
			background: green;
			
		}
		.right {
			position: absolute;
			top: 0px;
			right: 0px;
			width: 200px;
			background: blue;
		}
		.content {
			background: red;
			margin: 0 200px;
		}
        <div class="wrapper">
 	        <div class="content common">
		        <h1>Content</h1>
	        </div>
	        <div class="left common">
		        <h1>Left</h1>
	        </div>
	        <div class="right common">
		        <h1>Right</h1>
	        </div>
         </div>
 - **flex**
		html, body {
			height: 100%;
		}
		.wrapper {
			height: 80%;
			display: flex;
		}
		.common {
			height: 100%;
			color: white;
		}
		.content {
			flex-grow: 1;
			background: red;
		}
		.left {
			flex: 0 1 200px;
			order: -1;
			background: blue;
		}
		.right {
			flex: 0 1 200px;
			background: green;
		}
        <div class="wrapper">
	        <div class="content common">
		        <h1>Content</h1>
	        </div>
	        <div class="left common">
		        <h1>Left</h1>
	        </div>
	        <div class="right common">
		        <h1>Right</h1>
	        </div>
        </div>

总结
--
总结发现实现两栏或者三栏布局的方法大概有这么几种

 1. **脱离文档流+margin**
    在上面的实现方式中使用float和position:absolute来脱离文档流，然后再让剩下的元素调整外边距margin来做成自适应。
    
 2. **脱离文档流+触发BFC**
    使用float脱离文档流之后，我们再利用BFC区域不会与浮动元素重叠的特性来使剩下的元素自适应。
 3. **纯绝对定位**
    所有的栏都设置position:absolute，然后定宽元素设置宽度、left和Right位置，自适应元素只设置left和right位置
    
 4. **flex**
    使用flex的flex-grow和flex-shrink可以来实现自适应布局
 5. **其他**
    类似双飞翼和圣杯布局其实也是部分利用了浮动和定位的知识，以及负margin相关的操作，总体的知识并不变化
    

    	
    