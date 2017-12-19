<template>
	<!-- App -->
	<div id="app">

		<!-- Statusbar -->
		<div class="statusbar-overlay layout-dark"></div>
		<!--<f7-statusbar></f7-statusbar>-->



		<!-- Main Views -->
		<f7-views>
			<f7-view id="main-view" navbar-through :dynamic-navbar="true" main>

				<!-- Pages -->
				<f7-pages>
					<f7-page class="custom-page">

						<h1 class="ibm"></h1>

						<!--<div class="content-block row">-->

							<!--&lt;!&ndash; Default preloader &ndash;&gt;-->
							<!--<div style="text-align: center;">-->
								<!--<span class="preloader"></span>-->
							<!--</div>-->

						<!--</div>-->


						<!--<a @click="fetchArticles()">Fetch news</a>-->


						<form class="list-block">
							<ul>
								<!-- Text Input -->
								<li>
									<div class="item-content custom-form">
										<div class="item-inner">
											<div class="item-title label custom-label">Your name</div>
											<div class="item-input">
												<input type="text" placeholder="Vamsi"></div>
										</div>
									</div>
								</li>
								<!-- Password -->
								<li>
									<div class="item-content custom-form">
										<div class="item-inner">
											<div class="item-title label custom-label">Your crush</div>
											<div class="item-input">
												<input type="text" placeholder="Mounica"></div>
										</div>
									</div>
								</li>

							</ul>

						</form>


						<div class="content-block">
							<f7-button big raised fill color="red">Calculate love</f7-button>
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
                news : []
			}
        },

        methods: {

            fetchArticles() {


                axios.get('https://newsapi.org/v2/top-headlines?sources=techcrunch,the-next-web,mashable&apiKey=77053730ff024682b1ed50eb49243626')
                    .then(response => {
                        this.news = response.data.articles;

                    }, error => {
                        console.log(error);
                    });

            }

        },

		mounted: function() {
            this.fetchArticles();
		}

    }
</script>


<style lang="scss">
	@import "../node_modules/@ibm/type/css/ibm-type.min.css";

	.layout-dark .page.custom-page{
		background-color: #22232D;
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
