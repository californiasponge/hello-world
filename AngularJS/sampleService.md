        (function () {
            'use strict';

            angular.module('MyApp')
                .service('BlogsService', BlogsService);

            BlogsService.$inject = ['$http'];

            function BlogsService($http) {

                const blogEndpoint = '/api/blogs/'
                const categoryEndpoint = '/api/blogcategories/'

                this.getAllBlogPosts = () => {

                    return $http({
                        method: 'GET',
                        url: blogEndpoint,
                        withCredentials: true
                    });

                }

                this.getAllCategories = () => {

                    return $http({
                        method: 'GET',
                        url: categoryEndpoint,
                        withCredentials: true
                    })
                }

                this.createNewPost = (postRequest) => {

                    return $http({
                        method: 'POST',
                        url: blogEndpoint,
                        data: postRequest,
                        withCredentials: true
                    });

                }

                this.createNewCategory = (addCat) => {

                    return $http({
                        method: "POST",
                        url: categoryEndpoint,
                        data: addCat,
                        withCredentials: true
                    });

                }

                this.selectPostToEdit = (id) => {

                    return $http({
                        method: 'GET',
                        url: blogEndpoint + "blog/" + id,
                        withCredentials: true
                    });

                }

                this.selectCategory = (id) => {

                    return $http({
                        method: "GET",
                        url: categoryEndpoint + id,
                        withCredentials: true
                    });

                }

                this.editPost = (entry) => {

                    return $http({
                        method: 'PUT',
                        url: blogEndpoint + entry.id,
                        data: entry,
                        withCredentials: true
                    });
                }

                this.editCategory = (category) => {

                    return $http({
                        method: 'PUT',
                        url: categoryEndpoint + category.id,
                        data: category,
                        withCredentials: true
                    });
                }

                this.deletePost = (id) => {

                    return $http({
                        method: 'DELETE',
                        url: blogEndpoint + id,
                        withCredentials: true
                    });
                }

                this.deleteCategory = (id) => {

                    return $http({
                        method: 'DELETE',
                        url: categoryEndpoint + id,
                        withCredentials: true
                    });
                }

                this.getBlogPages = (page) => {
                    return $http({
                        method: 'GET',
                        url: blogEndpoint + "blogs-page=" + page,
                        withCredentials: true
                    })
                };

            }
        })();
