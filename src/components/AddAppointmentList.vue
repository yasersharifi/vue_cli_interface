<template>
	<div class="col-12">
		<div class="card textcenter mt-3">
			<div class="card-header bg-primary text-white addBtnArea" @click="$emit('show')">
				<font-awesome-icon icon="plus" class="ms-3"/>افزودن قرار ملاقات
			</div>

			<div class="card-body" v-if="active">
				<form id="aptForm" @submit.prevent="addRequest">
					<div class="row">
						<div class="form-group form-row col-6">
							<label class="col-form-label text-md-right" for="petName">نام حیوان</label>
							<div>
								<input
									type="text"
									class="form-control"
									name="petName"
									id="petName"
									placeholder="نام حیوان"
									v-model="formData.petName"
								>
							</div>
						</div>

						<div class="form-group form-row col-6">
							<label class="col-form-label text-md-right" for="ownerName">صاحب</label>
							<div class="">
								<input
									type="text"
									class="form-control"
									id="ownerName"
									placeholder="صاحب"
									v-model="formData.petOwner"
								>
							</div>
						</div>

						<div class="form-group col-6">
							<label class="col-form-label text-md-right" for="aptDate">تاریخ</label>
							<div class="">
								<input type="date" class="form-control" id="aptDate" v-model="formData.aptDate">
							</div>
						</div>
						<div class="form-group col-6">
							<label class="col-form-label text-md-right" for="aptTime">زمان</label>
							<div class="">
								<input
									type="time"
									class="form-control"
									name="aptTime"
									id="aptTime"
									v-model="formData.aptTime"
								>
							</div>
						</div>

						<div class="form-group col-12">
							<label class="text-md-right" for="aptNotes">توضیحات</label>
							<div class="">
								<textarea class="form-control" id="aptNotes" v-model="formData.aptNotes"></textarea>
							</div>
						</div>

						<div class="form-group form-row mb-0 mt-3">
							<div class="col-md-10">
								<button type="submit" class="btn btn-success d-block ml-auto">افزودن</button>
							</div>
						</div>
					</div>
				</form>
			</div>
		</div>
	</div>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
	name: "AddAppointmentList",
	data: function () {
		return {
			formData: [],
		}
	},
	props: ["active"],
	components: {
		FontAwesomeIcon,
	},
	methods: {
		addRequest: function () {
			this.formData = {
				petName: this.formData.petName,
				aptDate: this.formData.aptDate + " " + this.formData.aptTime,
				petOwner: this.formData.petOwner,
				aptNotes: this.formData.aptNotes,
			};
			this.$emit('add', this.formData);
			this.formData = [];
		}
	}
}
</script>

<style scoped>
.addBtnArea {
	cursor: pointer;
}
</style>