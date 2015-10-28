###Custom Pagination Directive

```javascript
(function(){
	angular.module('ng-pagination',[])
	.directive('pagination',function(){
	return {
		restrict:'E',
		scope: true,
		template:function(){
			var html='';
			//html+='numRecords:{{numRecords}},itemsPerPage:{{itemsPerPage}} ';
			html+= '<input type="button" value="<<" ng-click="prev();">';
			html+= '<input type="button" ng-repeat="page in range()" value="{{page}}"  ng-class="page==currentPage?\'active\':\'\'" ng-click="setPage(page);">';
			html+= '<input type="button" value=">>" ng-click="next();">';			
			return html;
		},
		link:function(scope,element,attrs){				
			scope.numRecords=parseInt(attrs.numrecords) || 50;
			scope.itemsPerPage=parseInt(attrs.itemsperpage) || 10;
			scope.currentPage=parseInt(attrs.currentpage) || 1;
			scope.maxPages=parseInt(attrs.maxpages) || 5;				
			scope.init();
		},
		controller: function($scope) {
			$scope.init=function(){				
				$scope.itemsPerPage = Math.min($scope.numRecords, $scope.itemsPerPage);
				$scope.pages = Math.ceil($scope.numRecords/$scope.itemsPerPage);
				$scope.maxPages = Math.min($scope.maxPages,$scope.pages);
				$scope.currentPage = Math.min($scope.maxPages,$scope.currentPage);	
				$scope.pageChanged();				
			}
			$scope.range=function(){
				var pages=[];
				var padding  = Math.floor($scope.maxPages/2);
				var start = Math.max(1,$scope.currentPage-padding);
				var startIndex = start;
				for(var i=start;i<start+$scope.maxPages;i++){
					(i>$scope.pages)?pages.push(--startIndex):pages.push(i);					
				}				
				return pages.sort(function(a,b){
					return a>b;
				});
			};			
			$scope.prev = function(){
				$scope.currentPage=Math.max(--$scope.currentPage, 1);
				$scope.pageChanged();
			}			
			$scope.next = function(){
				$scope.currentPage=Math.min(++$scope.currentPage, $scope.pages);	
				$scope.pageChanged();
			}
			$scope.setPage = function(page){
				$scope.currentPage=page;
				$scope.pageChanged();
			}
			$scope.pageChanged = function() {	
				if($scope.$parent.pageChanged)$scope.$parent.pageChanged();
				$scope.$parent.start = (($scope.currentPage - 1) * $scope.itemsPerPage);
				$scope.$parent.end =  $scope.start+$scope.itemsPerPage;
			};		
		}		
	}
});
}())
```

##Usage
####HTML
```html
<div ng-controller="yourcontroller">
    <ANY ng-repeat="u in users.slice(start,end)"></ANY>
		<pagination numRecords="{{numRecords}}" itemsPerPage="5" currentPage="1" maxPages="10" ></pagination>			
	</div>
```
####JS
```javascript
angular.module('yourapp',['ng-pagination'])
```
