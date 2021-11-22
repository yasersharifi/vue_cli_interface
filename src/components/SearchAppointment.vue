<template>
	<div class="col-12">
		<div class="input-group my-3">
			<input
				id="SearchApts"
				placeholder="جستجو ..."
				type="text"
				class="form-control"
				aria-label="Search Appointments"
				v-model="searchTerm"
			>

			<button class="btn btn-primary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">مرتب سازی </button>
			<ul class="dropdown-menu">
				<li><a class="dropdown-item dropdown-item d-flex justify-content-between"
					@click="$emit('sortByKey', 'petName')">نام حیوان <font-awesome-icon icon="check" v-if="sortKey === 'petName'"/></a></li>
				<li><a class="dropdown-item dropdown-item d-flex justify-content-between"
					@click="$emit('sortByKey', 'petOwner')">نام صاحب <font-awesome-icon icon="check" v-if="sortKey === 'petOwner'"/></a></li>
				<li><hr class="dropdown-divider"></li>
				<li><a class="dropdown-item dropdown-item d-flex justify-content-between"
					@click="$emit('sortByType', 'asc')">صعودی <font-awesome-icon icon="check"  v-if="sortType === 'asc'"/></a></li>
				<li><a class="dropdown-item d-flex justify-content-between"
					@click="$emit('sortByType', 'desc')">نزولی <font-awesome-icon icon="check"  v-show="sortType === 'desc'"/></a></li>
			</ul>
		</div>
	</div>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
	name: "SearchAppointment",
	props: ["sortType", "sortKey"],
	data: function () {
		return {
			searchTerm: '',
		}
	},
	components: {
		FontAwesomeIcon
	},
	watch: {
		searchTerm: function (newValue) {
			this.$emit("search", newValue);
		}
	}
}
</script>

<style scoped>
.input-group>:not(:first-child):not(.dropdown-menu):not(.valid-tooltip):not(.valid-feedback):not(.invalid-tooltip):not(.invalid-feedback) {
	border-radius: 5px 0 0 5px !important;
}
.input-group:not(.has-validation)>.dropdown-toggle:nth-last-child(n+3), .input-group:not(.has-validation)>:not(:last-child):not(.dropdown-toggle):not(.dropdown-menu) {
	border-radius: 0 5px 5px 0 !important;
}
</style>