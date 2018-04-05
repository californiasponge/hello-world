    (function () {
        'use strict';

        angular.module('MyApp')
            .config(ConfigStates);

        ConfigStates.$inject = ['$stateProvider', '$urlRouterProvider'];

        function ConfigStates($stateProvider, $urlRouterProvider) {

            $stateProvider
                .state({
                    name: 'app.blogs',
                    url: '/blogs',
                    templateUrl: 'blogs.html',
                    controller: "BlogsController",
                    controllerAs: "b"
                })
                .state({
                    name: 'app.blogsReadOne',
                    url: '/blogs/{id}',
                    templateUrl: 'blogsReadMore.html',
                    controller: "BlogsController",
                    controllerAs: 'b'
                })
                .state({
                    name: 'app.blogsCreate',
                    url: '/createpost',
                    templateUrl: 'blogsCreate.html',
                    controller: "BlogCreateController",
                    controllerAs: "bc"
                })
                .state({
                    name: 'app.blogsCreate_edit',
                    url: '/createpost/{id}',
                    templateUrl: 'blogsCreate.html',
                    controller: "BlogCreateController",
                    controllerAs: "bc"
                })
                .state({
                    name: 'app.blogCategories',
                    url: '/categories',
                    templateUrl: 'blogCategories.html',
                    controller: "BlogCategoriesController",
                    controllerAs: "bcc"
                })
                .state({
                    name: 'app.blogCategories_edit',
                    url: '/categories/{id}',
                    templateUrl: 'blogCategories.html',
                    controller: "BlogCategoriesController",
                    controllerAs: "bcc"
                })

        }

    })();
