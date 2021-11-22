<template>
	<div class="col-12">
		<div class="list-group list-group-flush">
			<div
				v-for="(item, index) in appointments"
				:key="index"
				class="list-group-item d-flex align-items-start">
				<button @click="$emit('remove', index)" class="ms-2 btn btn-sm btn-danger" title="حذف">
					<font-awesome-icon icon="trash"/>
				</button>
				<div class="w-100">
					<div class="d-flex justify-content-between">
            <span class="h4 text-primary" contenteditable="true" @blur="$emit('edit', 'petName', index, $event.target.innerText)">
                {{item.petName}}
            </span>
						<span class="float-right">{{item.aptDate}}</span>
					</div>
					<div class="owner-name">
						<span class="font-weight-bold text-primary mr-1">صاحب: </span>
						<span contenteditable="true" @blur="$emit('edit', 'petOwner', index, $event.target.innerText)">
                  {{item.petOwner}}
            </span>
					</div>
					<div contenteditable="true" @blur="$emit('edit', 'aptNotes', index, $event.target.innerText)">
						{{item.aptNotes}}
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
	name: "AppointmentList",
	props: ["appointments"],
	components: {
		FontAwesomeIcon
	}
}
</script>