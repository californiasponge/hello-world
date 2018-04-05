      (function () {

          'use strict';

          MyAppVariable
              .controller('BlogsController', BlogsController)

          BlogsController.$inject = ['BlogsService', '$state', '$scope', '$sce', '$stateParams'];

          function BlogsController(BlogsService, $state, $scope, $sce, $stateParams) {
              var b = this;

              this.id;

              this.readMode = false;

              this.pageNumber = 1;

              this.pagination = () => {
                  BlogsService.getBlogPages(this.pageNumber).then(
                      response => {
                          this.posts = response.data.items;
                          this.totalPosts = Math.ceil(response.data.items[0].totalPosts / 4);
                      },
                      err => {
                          $.gritter.add({
                              title: 'Loading Error',
                              text: 'please check your connection and reload',
                              sticky: true,
                              time: '',
                              class_name: 'my-sticky-class'
                          });
                      }
                  );
              }
              this.pagination();


              $scope.$on('deleteId', (event, id) => {
                  this.id = id;
              })

              b.trust = $sce.trustAsHtml;

              BlogsService.getAllBlogPosts().then(
                  response => {
                      b.blogPosts = response.data.items;
                  },

                  err => {
                      $.gritter.add({
                          title: 'Loading Error',
                          text: 'please check your connection and reload',
                          sticky: true,
                          time: '',
                          class_name: 'my-sticky-class'
                      });
                  }
              )


              BlogsService.getAllCategories().then(
                  response => {

                      this.blogCategories = response.data.items;

                  },

                  err => {
                      $.gritter.add({
                          title: 'Loading Error',
                          text: 'please check your connection and reload',
                          sticky: true,
                          time: '',
                          class_name: 'my-sticky-class'
                      });
                  }
              )

              b.selectPost = (id) => {

                  $state.go('app.blogsCreate_edit', { id: id })

              }

              b.readMore = (id) => {

                  $state.go('app.blogsReadOne', { id: id })

              }

              //move to read one mode
              if ($stateParams.id) {

                  this.readMode = true;

                  BlogsService.selectPostToEdit($stateParams.id).then(

                      response => {
                          b.id = response.data.item.id
                          b.dateCreated = response.data.item.dateCreated;
                          b.dateModified = response.data.item.dateModified;
                          b.firstName = response.data.item.firstName;
                          b.lastName = response.data.item.lastName;
                          b.title = response.data.item.title;
                          b.post = response.data.item.contents;
                      },

                      err => {
                          $.gritter.add({
                              title: 'Loading Error!',
                              text: 'Unable to Select. Please try a selection again',
                              sticky: true,
                              time: '',
                              class_name: 'my-sticky-class'
                          });
                      }

                  );
              }


              b.idForDelete = (id) => {

                  BlogsService.selectPostToEdit(id).then(
                      response => {

                          $scope.$broadcast("deleteId", id);

                          swal({
                              title: "Are you sure you want to delete this post?",
                              text: "The following action is permanent! Once deleted, you will not be able to recover this blog post. Please confirm that this is the action you would like to take.",
                              type: "error",
                              showCancelButton: true,
                              showCancelButtonText: 'No, go back!',
                              confirmButtonClass: 'btn-danger',
                              confirmButtonText: 'Yes, Delete!'
                          },
                              function (isConfirm) {
                                  if (isConfirm) {
                                      b.deleteSelectedPost();
                                  }
                              }
                          );
                      },

                      err => {
                          $.gritter.add({
                              title: 'Sorry, Cannot Select Item.',
                              text: ' Please try again',
                              sticky: true,
                              time: '',
                              class_name: 'my-sticky-class'
                          });
                      }

                  );
              }

              b.deleteSelectedPost = () => {
                  const id = this.id;

                  function post(obj) {
                      //unique obj identifier
                      return obj.id == id;

                  }

                  const index = this.posts.findIndex(post);

                  BlogsService.deletePost(id).then(
                      response => {

                          $.gritter.add({
                              title: 'DELETE SUCCESS!',
                              text: 'Your post has been successfully deleted.',
                              sticky: false,
                              time: '',
                              class_name: 'my-sticky-class'
                          });
                          this.posts.splice(index, 1);

                      },
                      err => {

                          $.gritter.add({
                              title: 'Sorry, Could Not Delete Post.',
                              text: ' Please try again',
                              sticky: true,
                              time: '',
                              class_name: 'my-sticky-class'
                          });

                      }
                  );
              }


              //pagination cont'd
              this.previous = () => {
                  if (this.pageNumber > 1) {
                      this.pageNumber--;
                      this.pagination();
                  }
              };

              this.next = () => {
                  if (this.pageNumber < this.totalPosts) {
                      this.pageNumber++;
                      this.pagination();
                  }
              };

          }
      })();
