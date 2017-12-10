<template>
	<!-- App -->
	<div id="app">

		<!-- Statusbar -->
		<f7-statusbar></f7-statusbar>



		<!-- Main Views -->
		<f7-views>
			<f7-view id="main-view" navbar-through :dynamic-navbar="true" main>
				<!-- Navbar -->
				<f7-navbar title="News App" theme="#ffffff">



				</f7-navbar>
				<!-- Pages -->
				<f7-pages>
					<f7-page>

						<!--<div class="content-block row">-->

							<!--&lt;!&ndash; Default preloader &ndash;&gt;-->
							<!--<div style="text-align: center;">-->
								<!--<span class="preloader"></span>-->
							<!--</div>-->

						<!--</div>-->


						<!--<a @click="fetchArticles()">Fetch news</a>-->

						<div class="content-block-title">Top headlines</div>
						<div class="list-block media-list">
							<ul>
								<li v-for="article in news">
									<a href="/about" class="item-link item-content">
										<div class="item-media"><img v-bind:src="article.urlToImage" width="80"></div>
										<div class="item-inner">
											<div class="item-title-row">
												<div class="item-title">{{article.title}}</div>
												<div class="item-after"><timeago :since="article.publishedAt" :auto-update="0"></timeago></div>
											</div>
											<div class="item-subtitle">{{article.source.name}}</div>
											<div class="item-text">{{article.description}}</div>
										</div>
									</a>
								</li>

							</ul>
						</div>

						<!--<f7-swiper scrollbar>-->
							<!--<f7-swiper-slide v-for="article in news">-->

								<!--&lt;!&ndash;<img v-bind:src="article.urlToImage">&ndash;&gt;-->
								<!--<h1>{{article.title}}</h1>-->
								<!--<p>{{article.description}}</p>-->

							<!--</f7-swiper-slide>-->

						<!--</f7-swiper>-->
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


<style lang=scss>

</style>
