<template>
<div class="row" v-if="(!lockedOut || manuallyUnlocked)">
	<div class="col-md-2 fader-container">
		<cue-fader :cue="[1100,1105,1110,1115,1120,1125,1130,1135,1140,1145,1150,1155,1160,1165,1170,1175,1180,1185,1190,1195,1199]" v-bind:activeQueList="$root.activeCuelists" name="Row 1" type="House Lights"></cue-fader>
	</div>
	<div class="col-md-2 fader-container">
		<cue-fader :cue="[1200,1205,1210,1215,1220,1225,1230,1235,1240,1245,1250,1255,1260,1265,1270,1275,1280,1285,1290,1295,1299]" v-bind:activeQueList="$root.activeCuelists" name="Row 2" type="House Lights"></cue-fader>
	</div>
	<div class="col-md-2 fader-container">
		<cue-fader :cue="[1300,1305,1310,1315,1320,1325,1330,1335,1340,1345,1350,1355,1360,1365,1370,1375,1380,1385,1390,1395,1399]" v-bind:activeQueList="$root.activeCuelists" name="Row 3" type="House Lights"></cue-fader>
	</div>
	<div class="col-md-2 fader-container">
		<cue-fader :cue="[1400,1405,1410,1415,1420,1425,1430,1435,1440,1445,1450,1455,1460,1465,1470,1475,1480,1485,1490,1495,1499]" v-bind:activeQueList="$root.activeCuelists" name="Row 4" type="House Lights"></cue-fader>
	</div>

	<div class="col-md-4">
		<cue-button :cue="12" name="Pre/Post Service" type="Presets" color="bg-green" icon="fa-star"></cue-button>
		<cue-button :cue="13" name="Worship" type="Presets" color="bg-green" icon="fa-star"></cue-button>
		<cue-button :cue="14" name="Sermon" type="Presets" color="bg-green" icon="fa-star"></cue-button>
		<cue-button :cue="11" name="All Off" type="Presets" color="bg-red" icon="fa-power-off"></cue-button>
	</div>
</div>
<div v-else>
	<div class="lockscreen-wrapper">
		<div class="lockscreen-logo">Auditorium Lighting</div>

		<div class="text-center" style="margin-bottom: 24px;">
			Loading scenes...
		</div>
		<p class="text-center" style="font-size: 36px; margin-bottom: 24px;">
			<i class="fa fa-refresh fa-spin"></i>
		</p>
	</div>

</div>
</div>
</template>

<script>
module.exports = {
	computed: {
		cuelistsLoaded: function() {
			return this.$parent.$data.cuelistsLoaded;
		},
		lockedOut: function() {
			return this.$parent.$data.lockedOut;
		},
		manuallyUnlocked: function() {
			return this.$parent.$data.manuallyUnlocked;
		}
	}
}
</script>

<style>


	body.fixed .content-wrapper {
		height: 100vh;
		padding: 0;
	}

	body.fixed section.content {
		height: 100%;
	}

	body.fixed section.content .row {
		height: 100%;
	}

	body.fixed section.content .row .fader-container {
		height: 100%;
	}
</style>
