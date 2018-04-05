**SIMPLE FORM WITH VALIDATION AND TEXT EDITOR PLUGIN**    
    
    <!-- begin form panel -->
    <div class="col-md-10">
        <div class="panel panel-inverse">
            <div class="panel-heading" style="width: 100%">
                <h4 class="panel-title">Blog Post Form</h4>
            </div>
            <br />
            <div class="panel-body">
                <!-- begin form -->
                <form class="form-horizontal col-md-10" id="createForm" name="bc.formData" novalidate="">
                    <input type="text" name="postId" class='hidden' ng-model="bc.postId" />
                    <h3>CREATE A POST</h3>
                    <hr />

                    <div class="form-group has-feedback" ng-class="bc.getValidationClass('title')">
                        <label class="col-md-3 control-label">Blog Entry Title
                            <span class="text-danger">*</span>
                        </label>
                        <div class="col-md-6">
                            <input ng-model="bc.title" ng-blur="bc.save()" type="text" class="form-control" name="title" required placeholder="Title"
                            />
                            <span class="fa form-control-feedback" ng-class="bc.getValidationClass('title')"></span>
                        </div>
                    </div>
                    <br />
                    <div class="form-group has-feedback" ng-class="bc.getValidationClass('authorFirstName')">
                        <label class="col-md-3 control-label">Author First Name
                            <span class="text-danger">*</span>
                        </label>
                        <div class="col-md-6">
                            <input ng-model="bc.authorFirstName" ng-blur="bc.save()" type="text" class="form-control ng-pristine ng-untouched ng-empty ng-invalid ng-invalid-required"
                                name="authorFirstName" required placeholder="First Name" />
                            <span ng-class="bc.getValidationClass('authorFirstName')" class="fa form-control-feedback"></span>
                        </div>
                    </div>
                    <br />
                    <div class="form-group has-feedback" ng-class="bc.getValidationClass('authorLastName')">
                        <label class="col-md-3 control-label">Author Last Name
                            <span class="text-danger">*</span>
                        </label>
                        <div class="col-md-6">
                            <input ng-model="bc.authorLastName" ng-blur="bc.save()" type="text" class="form-control ng-pristine ng-untouched ng-empty ng-invalid ng-invalid-required"
                                name="authorLastName" required placeholder="Last Name" />
                            <span ng-class="bc.getValidationClass('authorLastName')" class="fa form-control-feedback"></span>
                        </div>
                    </div>
                    <br />

                    <div class="form-group" ng-class="bc.getValidationClass('selectedCategory')">
                        <label class="control-label col-sm-3">Blog Category
                            <span class="text-danger">*</span>
                        </label>
                        <div class="col-sm-6">
                            <select ng-blur="bc.save()" required ng-model="bc.selectedCategory" name="selectedCategory" ng-options="category.categoryId as category.categoryName for category in bc.blogCategories">
                                <option value="" disabled>--Please Select a Category--</option>
                            </select>
                            <span ng-class="bc.getValidationClass('selectedCategory')" class="fa form-control-feedback"></span>
                        </div>
                    </div>
                    <br />
                    <div class="form-group has-feedback" ng-class="bc.getValidationClass('message')">
                        <label class="col-md-3 control-label">Blog Content
                            <span class="text-danger">*</span>
                        </label>
                    </div>
                    <lms-editor ng-blur="bc.save()" name="message" editor-contents='bc.summernote'></lms-editor>
                </form>


                <div style="margin: 10px" class="col-md-10">

                    <button ng-if="bc.editMode" ng-model='bc.updateBtn' type="submit" class="pull-right btn btn-sm btn-success" ng-click='bc.submitEdit(id)'>UPDATE ENTRY</button>

                    <button ng-disabled="bc.formData.$invalid" ng-if="!bc.editMode" ng-model='bc.sendBtn' type="submit" class="pull-right btn btn-sm btn-success"
                        ng-click='bc.createNewPost()'>SUBMIT BLOG ENTRY</button>


                    <button type="button" ng-click="bc.cancel()" style="margin-right: .5em" class="pull-right btn btn-sm btn-default" ui-sref='app.blogs'>CANCEL</button>
                </div>

                <!-- end form -->

            </div>
        </div>
    </div>
    <!-- end form panel -->
