### Table of Contents
* [Controllers](#controllers)
* [Services](#services)
* [Directives](#directives)

## Controllers

```js
describe('Controller: controllerName', function () {

    var ctrl, scope, injectedServiceVariableName ;
    
    // Step 1: Import the module this controller belongs to, and its dependencies
    beforeEach(function() {
        module('moduleName1');
        module('moduleName2');
        module('moduleName3');
    });

    // Step 2: Mock any service that initially used when the controller instantiate
    beforeEach(module(function($provide) {

        $provide.value('mockedServiceName', {
            propertyName: value,
            propertyName: value
        });

    }));

    // Step 3: Inject $controller with its dependencies

    beforeEach(inject(function ($rootScope, $controller, _injectedServiceName_) {
        scope = $rootScope.$new();
        ctrl= $controller('controllerName', {$scope: scope});
        injectedServiceVariableName = _injectedServiceName_
    }));

    // Step 4: Test the controller

    it('controller should be defined', function () {
        expect(ctrl).toBeDefined();
    });

});
```

## Services

```js
describe('Service: serviceName', function() {
    var serviceNameVariable;

    // Step 1: Import the module this service belongs to
    beforeEach(function() {
        module('moduleName1');
        module('moduleName2');
        module('moduleName3');
    });

    // Step 2: Before each test set our injected service to our local Service variable
    beforeEach(inject(function(_serviceName_) {
        serviceNameVariable = _serviceName_;
    }));

    // Step 3: A simple test to verify the Users factory exists
    it('Service Should be defined', function() {
        expect(serviceName).toBeDefined();
    });
});
```

## Directives

```js
describe('Directive: directiveName', function() {

    var scope, element, directiveElem;

    function getCompiledElement(template) {
        element = angular.element(template);
        element = compile(element)(scope);
        scope.$digest();
        return element;
    }
    // 1. Load the module
    beforeEach(function() {
        module('moduleName');

        inject(function($compile, $rootScope) {
            compile = $compile;
            scope = $rootScope.$new();
        });

        directiveElem = getCompiledElement();
    });

    // 2. Inject $rootScope and $compile
    beforeEach(inject(function($rootScope, $compile) {
        getCompiledElement('<directiveName>This is message title</directiveName>');
    }));

    // 7. Test that it worked

    it('should have transclude content', function() {
        expect(element.find('span').length).toEqual(3);
    });
});
```