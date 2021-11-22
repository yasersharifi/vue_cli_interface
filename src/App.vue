<template>
	<div id="app" class="container mt-4">
		<div class="row justify-content-center">
			<div class="col-12 col-md-10 col-lg-7">
				<div class="card" style="box-shadow: 0 0 42px 10px #c6c4c4ee !important;border: 0 !important;">
					<div class="card-body">
						<alert v-if="isAlert"
						:alert-class="alertClass"
						:alert-text="alertText"
						:is-alert="isAlert"
						:alert-counter="alertCounter"
						@hide="hideAlert"/>
						<add-appointment-list
							:active="activeAddArea"
							@show="showAddArea"
							@add="addAppointmentList"/>
						<search-appointment
							@search="searchAppointment"
							@sortByKey="sortByKey"
							@sortByType="sortByType"
							:sort-type="sortType"
							:sort-key="sortKey"/>
						<AppointmentList
							:appointments="searchItems"
							@remove="deleteAppointment"
							@edit="editItem"/>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from "axios";

import AppointmentList from "./components/AppointmentList";
import AddAppointmentList from "./components/AddAppointmentList";
import Alert from "./components/Alert";
import SearchAppointment from "./components/SearchAppointment";

export default {
	name: 'App',
	data: function () {
		return {
			title: "Appointment List",
			appointments: [],
			activeAddArea: false,

			isAlert: false,
			alertText: "",
			alertClass: "",
			alertCounter: 3,

			searchString: "",

			sortType: "asc",
			sortKey: "petOwner"
		}
	},
	components: {
		AppointmentList,
		AddAppointmentList,
		Alert,
		SearchAppointment
	},
	mounted() {
		axios
			.get("./data/appointments.json")
			.then(response => (this.appointments = response.data));
	},
	computed: {
		searchItems: function () {
			return this.appointments.filter(item => {
				return (
					item.petName.toLowerCase().match(this.searchString.trim().toLowerCase()) ||
					item.petOwner.toLowerCase().match(this.searchString.trim().toLowerCase()) ||
					item.aptNotes.toLowerCase().match(this.searchString.trim().toLowerCase())
				);
			}).sort(this.compare);
		}
	},
	methods: {
		deleteAppointment: function (index) {
			this.appointments.splice(index, 1);
		},
		editItem: function (editItem, index,  newData) {
			this.isAlert = false;
			this.alertCounter = 3;
			this.appointments[index][editItem] = newData;

			this.isAlert = true;
			this.alertClass = "alert-success";
			this.alertText = "Edited Successfully !!!";
			this.counterReduce(this);
			setTimeout(() => this.hideAlert(), 3000);
		},
		showAddArea: function () {
			this.activeAddArea = ! this.activeAddArea;
		},
		hideAlert: function () {
			this.isAlert = false;
			this.alertClass = "";
			this.alertText = "";
		},
		counterReduce: function (self) {
			let counterInterval = setInterval(function () {
				if (self.alertCounter <= 0) {
					clearInterval(counterInterval);
					self.alertCounter = 3;
				} else {
					self.alertCounter --;
				}
			}, 1000);
		},
		addAppointmentList: function (formData) {
			this.appointments.unshift(formData);
			this.activeAddArea = false;
		},
		searchAppointment: function (value) {
			this.searchString = value;
		},
		compare: function (a, b) {
			let returnValue = 0;
			let key = this.sortKey;
			if ( a[key] < b[key] ){
				if (this.sortType === "asc") {
					returnValue = 1;
				} else {
					returnValue = -1;
				}
			}
			if ( a[key] > b[key] ){
				if (this.sortType === "desc") {
					returnValue = -1;
				} else {
					returnValue = 1;
				}
			}
			return returnValue;
		},
		sortByKey: function (key) {
			this.sortKey = key;
		},
		sortByType: function (type) {
			this.sortType = type;
		}
	}
}
</script>
