<template lang="html">
	<section class="content">
		<div class="row">
			<div class="col-md-12">
				<box-table :links="links" :params="params" :source="source" :title="title" :thead="thead">
					<template slot-scope="props">
						<tr>
							<td>{{ props.item.title }}</td>
							<td>{{ props.item.user.name }}</td>
							<td></td>
							<td>
								<label for="" class="label label-success" v-if="props.item.status === 1">Active</label>
								<label for="" class="label label-danger" v-else>Draft</label>
							</td>
							<td>{{ props.item.date | moment("d/m/Y") }}</td>
							<td>
								<a href="javascript:void(0)" v-on:click="editUser(id = props.item.id)" class="btn btn-sm btn-primary"><i class="fa fa-edit"></i></a>
							</td>
						</tr>
					</template>
				</box-table>
			</div>
		</div>
	</section>
</template>

<script>
	import BoxTable from '~/lib/BoxTable.vue'
	export default {
		components: { BoxTable },
		data(){
			return{
				links: [
				{label: 'All', className: 'btn btn-default btn-sm', link : '/pages/all'},
				{label: 'Published', className: 'btn btn-primary btn-sm', link : '/pages'},
				{label: 'Draft', className: 'btn btn-warning btn-sm', link : '/pages/draft'},
				{label: 'Trash', className: 'btn btn-danger btn-sm', link : '/pages/trashed'},
				{label: 'Create', className: 'btn btn-success btn-sm', link : '/pages/create'}
				],
				source: '/adcom-json/pages',
				title: 'Published',
				thead: [
				{label: 'Title'},
				{label: 'Author'},
				{label: 'Categories'},
				{label: 'Status'},
				{label: 'Date'},
				{label: 'Action'}
				],
				params: {
				    column: 'id',
	                direction: 'desc',
	                status: 1,
	                status_2: '',
	                per_page: 10,
	                page: 1,
	                search_column: 'username',
	                search_operator: 'equal_to',
	                search_query_1: '',
	                search_query_2: ''
				}
			}
		},
		methods: {
			editUser: function(id){
				this.$router.push('/pages/' + id + '/edit')
			}
		}
	}
</script>