<script setup>
import { ref } from 'vue';
	// Sample student data
const students = ref([
    { id: 1, name: 'សុខ វិចិត្រ', class: 'Grade 10A', status: 'Present' },
    { id: 2, name: 'ចន្ទ សុភា', class: 'Grade 10A', status: 'Absent' },
    { id: 3, name: 'ពិរុណ សុវណ្ណ', class: 'Grade 10B', status: 'Late' },
    { id: 4, name: 'សុវណ្ណ មករា', class: 'Grade 10B', status: 'Present' },
    { id: 5, name: 'រដ្ឋា កញ្ញា', class: 'Grade 11A', status: 'Present' }
]);
</script>
<template>
	<div>
				<h2 class="text-xl font-semibold text-gray-800 mb-4">
					Students List
	</h2>
	<div class="overflow-x-auto">
					<table class="min-w-full divide-y divide-gray-200">
									<thead class="bg-gray-50">
													<tr>
																	<th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
																	<th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Class</th>
																	<th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
													</tr>
									</thead>
									<tbody class="bg-white divide-y divide-gray-200">
													<tr v-for="student in students" :key="student.id">
																	<td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
																					{{ student.name }}
																	</td>
																	<td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
																					{{ student.class }}
																	</td>
																	<td class="px-6 py-4 whitespace-nowrap">
																					<span :class="{
																									'px-2 inline-flex text-xs leading-5 font-semibold rounded-full': true,
																									'bg-green-100 text-green-800': student.status === 'Present',
																									'bg-red-100 text-red-800': student.status === 'Absent',
																									'bg-yellow-100 text-yellow-800': student.status === 'Late'
																					}">
																									{{ student.status }}
																					</span>
																	</td>
													</tr>
									</tbody>
					</table>
	</div>
	</div>
</template>



<style lang="scss" scoped>

</style>