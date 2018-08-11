<template>
<div class="row" v-if="(!lockedOut || manuallyUnlocked)">
	<div class="col-md-2 fader-container">
		<cue-fader :cue="[11,12,13,14]" v-bind:activeQueList="$root.activeCuelists" name="Row 1" type="House Lights"></cue-fader>
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