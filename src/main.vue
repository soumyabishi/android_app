<template>
	<!-- App -->
	<div id="app">

		<!-- Statusbar -->
		<div class="statusbar-overlay layout-dark"></div>
		<!--<f7-statusbar></f7-statusbar>-->



		<!-- Main Views -->
		<f7-views>
			<f7-view id="main-view" navbar-through :dynamic-navbar="false" main>


				<!-- Pages -->
				<f7-pages no-navbar="true">
					<f7-page class="custom-page">


						<f7-navbar theme="22232D" no-shadow>
							<f7-nav-left>
								<f7-link icon="icon-bars" open-panel="right"></f7-link>
							</f7-nav-left>
							<f7-nav-center></f7-nav-center>
							<f7-nav-right>
								<!--<f7-link icon-material="icon-bars" open-panel="right"></f7-link>-->
							</f7-nav-right>
						</f7-navbar>


						<h1 class="ibm"></h1>


						<form class="list-block">
							<ul>
								<!-- Text Input -->
								<li>
									<div class="item-content custom-form">
										<div class="item-inner">
											<div class="item-title label custom-label">Your name</div>
											<div class="item-input">
												<input type="text" placeholder="Vamsi" v-model="yourName"></div>
										</div>
									</div>
								</li>
								<!-- Password -->
								<li>
									<div class="item-content custom-form">
										<div class="item-inner">
											<div class="item-title label custom-label">Your crush</div>
											<div class="item-input">
												<input type="text" placeholder="Mounica" v-model="crushName"></div>
										</div>
									</div>
								</li>

							</ul>



						</form>


						<div class="content-block">

							<a href="#" v-bind:class="{ disabled: (yourName.length==0 || crushName.length==0)}" class="color-red button-fill button-big button-raised button"
							   v-bind:href="''+ '/match?fname=' + yourName + '&' + 'sname='+ crushName+ ''">Calculate love</a>

						</div>





					</f7-page>
				</f7-pages>


			</f7-view>
		</f7-views>









	</div>
</template>

<script>
    import axios from "axios";
    import Vue from 'vue';
    import VueTimeago from 'vue-timeago';
    Vue.use(VueTimeago, {
        name: 'timeago', // component name, `timeago` by default
        locale: 'en-US',
        locales: {
            // you will need json-loader in webpack 1
            'en-US': require('vue-timeago/locales/en-US.json')
        }
    })


    export default {
        data() {
            return {
                yourName : '',
				crushName :''

            }
        },

    }
</script>


<style lang="scss">
	@import "../node_modules/@ibm/type/css/ibm-type.min.css";

	.layout-dark .page.custom-page, .theme-red .navbar{
		background-color: #22232D;

		.list-block ul:before{
			display: none;
		}
	}




	.custom-form{

		.focus-state.item-inner .label{
			color: #fff !important;
		}
		.custom-label{
			text-transform: uppercase !important;

		}
		input{
			height: 66px !important;
			font-size: 39px !important;
		}
	}


</style>
