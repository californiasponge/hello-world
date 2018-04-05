**COMPONENT FOR LOGOUT BUTTON**  

    (function () {
        'use strict';

        MyAppVariable.component('logout', {
            templateUrl: 'logout.html',
            controller: LogoutController
        });

        LogoutController.$inject = ['UsersService', '$state'];

        function LogoutController(UsersService, $state) {

            this.logout = () => {
                UsersService.logout().then(
                    response => {
                        $.gritter.add({
                            title: 'Logout Successful!',
                            text: 'See you soon for your next match!',
                            sticky: false,
                            time: '',
                            class_name: 'my-sticky-class'
                        });

                        $state.go('login')
                    },
                    err => {
                        swal({
                            title: "Unable to logout",
                            text: "Please try again",
                            type: "error"
                        });
                    }
                )
            }
        }
    })();
