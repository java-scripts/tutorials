
```javascript
var Paging = function(config){
		
	var start, end;		
			
	var settings={
		numRecords:50,
		itemsPerPage:10,
		currentPage:1,
		maxPages:5	
	};
	
	var extend = function(dst,src){
		for(var k in src){
			dst[k]=src[k];
		}
	};	
	
	var _init = function(){
		extend(settings, config);				
		settings.itemsPerPage = Math.min(settings.numRecords, settings.itemsPerPage);
		settings.pages = Math.ceil(settings.numRecords/settings.itemsPerPage);
		settings.maxPages = Math.min(settings.maxPages,settings.pages);
		settings.currentPage = Math.min(settings.maxPages,settings.currentPage);				
		_pageChanged.call(this);
	};	
	
	
	var _pageChanged = function(){		
		this.start = ((settings.currentPage - 1) * settings.itemsPerPage);
		this.end =  this.start+settings.itemsPerPage;	
		this.pages=_getPages();
		this.currentPage=settings.currentPage;			
	};
	
	this.setPage = function(page){
		if(page=='prev'){
			settings.currentPage=Math.max(--settings.currentPage, 1);
		}else if(page=='next'){
			settings.currentPage=Math.min(++settings.currentPage, settings.pages);
		}else{
			settings.currentPage=page*1;
		}				
		_pageChanged.call(this);
		return this;
	};
			
	var _getPages=function(){
		var pages=[];
		var padding  = Math.floor(settings.maxPages/2);
		var start = Math.max(1,settings.currentPage-padding);
		var startIndex = start;
		for(var i=start;i<start+settings.maxPages;i++){
			(i>settings.pages)?pages.push(--startIndex):pages.push(i);					
		}				
		return pages.sort(function(a,b){
			return a>b;
		});
	};			
	_init.call(this);
};
```

####Example Usage
```javascript
//create an instance
var p = new Paging({numRecords:300,itemsPerPage:25,maxPages:10})
//invoke setpage method with a page number
p.setPage(9);//returns all we need
> Paging {start: 200, end: 225, pages: [3, 4, 5, 6, 7, 8, 9, 10, 11, 12], currentPage: 9}
```
