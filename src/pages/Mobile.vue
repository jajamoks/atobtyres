<template>
	<Layout>
		<div class="mobile-fitting">
			<Hero>
				<div class="row justify-content-between">
					<div class="col-md-4 col-sm-7">
						<h1><span class="marks">//</span>Mobile</h1>
						<p>
							Full Mobile Tyre Fitting Service. Same day mobile tyre services at your home, work or
							roadside assistance to get you back on the road.
						</p>
					</div>
					<div class="col-md-6 col-sm-5">
						<g-image src="~/assets/img/van.png" class="img-fluid" style="margin: -100px;"/>
					</div>
				</div>
			</Hero>
			<div>
				<div class="container">
					<div class="row justify-content-center main-text">
						<div class="col-md-12">
							<h2><span class="marks">//</span>Convenient</h2>
							<p>
								Tyre problems are a nightmare, and have a nasty habit of happening when they are
								least
								convenient.
								However, at A to B Tyres, we have a large range of machinery to get you back on the
								road.
								Whether it's at your home, your work or on the roadside, we're here to help.
							</p>
						</div>
						<div class="col-md-12">
							<h2><span class="marks">//</span>Affordable</h2>
							<p>
								We are a family run business and we have over 40 years experience in fixing and
								replacing tyres
								of all sizes. We know how annoying tyre issues can be, and that's why we'd love to
								help, at
								very affordable prices in Ipswich, Suffolk.
							</p>
						</div>
						<div class="col-md-12 mb-3">
							<h2><span class="marks">//</span>Same day call out and fitting</h2>
							<p>
								We understand your time is important, that's why as soon as one of our fitters is
								available
								they will come to your assistance the same day. We have a large number of tyres in
								stock for
								instant fitting, and if you order before 11am we can fit any tyre for same day
								delivery.
							</p>
						</div>
					</div>
					<div class="row">
						<div class="col-md-4">
							<img class="img-fluid" src="~/assets/img/mobile-1.jpg">
						</div>
						<div class="col-md-4">
							<img class="img-fluid" src="~/assets/img/mobile-2.jpg">
						</div>
						<div class="col-md-4">
							<img class="img-fluid" src="~/assets/img/mobile-3.jpg">
						</div>
						<div class="col-md-12">
							<b>
								We offer tyres fitting, tyre repairs, puncture repairs, leverless fitting, fixing
								cracked rims, replacing TPMS valves and other services both in our warehouse and on
								the road.
							</b>
						</div>
					</div>
				</div>
			</div>
			<ClientOnly>
				<GmapMap
						ref="mapRef"
						:center="{lat,lng}"
						:zoom="14"
						map-type-id="terrain"
						style="width: 100%; height: 400px"
						:options="{
						   zoomControl: true,
						   mapTypeControl: false,
						   scaleControl: false,
						   streetViewControl: false,
						   rotateControl: false,
						   fullscreenControl: false,
						   disableDefaultUi: true
						 }"
				>
					<GmapMarker
							:key="index"
							v-for="(m, index) in markers"
							:position="m.position"
							:clickable="true"
							:draggable="true"
							@click="center=m.position"
					/>
				</GmapMap>
			</ClientOnly>
		</div>
	</Layout>
</template>
<script>
	import config from 'config';
	import Hero from '~/components/Hero.vue'

	export default {
		metaInfo: {
			title: 'Mobile Fitting',
			meta: [
				{property: "og:type", content: 'article'},
				{property: "og:title", content: 'Mobile Fitting - ' + config.name},
				{property: "og:description", content: config.desc},
				{property: "og:url", content: config.url},
				{property: "og:image", content: config.url + 'static-contact.png'},
				{property: "twitter:card", content: "summary_large_image"},
				{property: "twitter:title", content: 'Contact - ' + config.name},
				{property: "twitter:description", content: config.desc},
				{property: "twitter:site", content: "@elementsworks"},
				{property: "twitter:creator", content: "@elementsworks"},
				{property: "twitter:image", content: config.url + 'static-contact.png'},
			]
		},
		components: {

			Hero
		},
		mounted: function () {
			console.log(this.lat, this.lng);

		},
		methods: {
			message: function (event) {
				FB.CustomerChat.show(true);
				FB.CustomerChat.update({
					logged_in_greeting: 'Got any questions or fancy a chat?',
					logged_out_greeting: 'Log in to chat with us.',
					ref: this.type,
				});
			},
			move(lat, lng) {
				console.log(lat, lng);
				this.lat = lat;
				this.lng = lng;
			}
		},
		data: function () {
			return {
				lat: 52.058529,
				lng: 1.125027,
				markers: [
					{
						position: {lat: 52.058529, lng: 1.125027},
						label: 'I',
						type: 'info'
					}
				]
			}
		}
	}
</script>

<style lang="scss">
	.animate {
		-webkit-transition: all 300ms linear;
		-moz-transition: all 300ms linear;
		-o-transition: all 300ms linear;
		-ms-transition: all 300ms linear;
		transition: all 300ms linear;
	}

	.mobile-fitting {
		.main-text {
			h2 {
				padding-top: 50px;
			}
			p {
				padding-bottom: 20px;
				font-size: 20px;
			}
		}
		img {
			margin: 20px 0;
		}

		b {
			text-align: center;
			margin: 20px auto;
			display: block;
			padding-bottom: 50px;
		}

	}

	// Extra small devices (portrait phones, less than 576px)
	@media (max-width: 575.98px) {
		.mobile-fitting {
			.main-text {
				p, h2 {
					padding: 0 30px;
				}
			}
			b {
				padding: 0 30px 20px;
			}
		}

	}

	// Small devices (landscape phones, less than 768px)
	@media (max-width: 767.98px) {

	}

	// Medium devices (tablets, less than 992px)
	@media (max-width: 991.98px) {

	}

	// Large devices (desktops, less than 1200px)
	@media (max-width: 1199.98px) {

	}
</style>
