<template>
    <nav class="navbar-default navbar-static-side" role="navigation">
        <div class="sidebar-collapse">
            <a class="close-canvas-menu"><i class="fa fa-times"></i></a>
            <ul class="nav metismenu" id="side-menu">
                <li v-for="item in menu">
                    <a :href="item.type == 'G' ? 'javascript:void(0)': item.full_url">
                        <i class="fa fa-th-large"></i>
                        <span class="nav-label">{{item.name}}</span>
                        <span class="fa arrow"></span>
                    </a>
                    <ul class="nav nav-second-level collapse" v-if="item.submenu">
                        <li v-for="subitem in item.submenu">
                            <a :href="subitem.type == 'G' ? 'javascript:void(0)': subitem.full_url">
                                {{subitem.name}}
                                <span class="fa arrow" v-if="subitem.submenu.length != 0"></span>
                            </a>
                            <ul class="nav nav-third-level collapse" v-if="subitem.submenu.length != 0">
                                <li v-for="subitem2 in subitem.submenu">
                                    <a :href="subitem2.type == 'G' ? 'javascript:void(0)': subitem2.full_url">
                                        {{subitem2.name}}
                                        <span class="fa arrow" v-if="subitem2.submenu.length != 0"></span>
                                    </a>
                                    <ul class="nav nav-third-level collapse" v-if="subitem2.submenu.length != 0">
                                        <li v-for="subitem3 in subitem2.submenu">
                                            <a :href="subitem3.type == 'G' ? 'javascript:void(0)': subitem3.full_url">
                                                {{subitem3.name}}
                                                <span class="fa arrow" v-if="subitem3.submenu.length != 0"></span>
                                            </a>
                                            <ul class="nav nav-third-level collapse" v-if="subitem3.submenu.length != 0">
                                                <li v-for="subitem4 in subitem3.submenu">
                                                    <a :href="subitem4.type == 'G' ? 'javascript:void(0)': subitem4.full_url">
                                                        {{subitem4.name}}
                                                    </a>
                                                </li>
                                            </ul>
                                        </li>
                                    </ul>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>

            </ul>

        </div>
    </nav>

</template>

<style>    
    .canvas-menu.mini-navbar .nav-second-level li a{
        padding-left: 30px;
    }
    .canvas-menu.mini-navbar .nav-third-level li a{
        padding-left: 40px;
    }
    .canvas-menu.mini-navbar .nav-third-level .nav-third-level li a{
        padding-left: 50px;
    }
</style>

<script>

export default {

    data(){
        return{
            menu: {}
        }
    },

    mounted: function(){
        this.getItensMenu();             
    },

    methods: {
        getItensMenu: function(){
            $.ajax({
                type: 'GET',
                dataType: 'json',
                headers: {
                    'Accept': 'application/json'
                },
                url: '/menu',
                success: data =>{ 
                    this.menu = data;
                    setTimeout(function(){
                        $('#side-menu').metisMenu();
                    },500)
                }
            });
        }
    }
}
</script>
