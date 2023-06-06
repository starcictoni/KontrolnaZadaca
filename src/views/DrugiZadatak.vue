<template>
	<v-container fill-height fluid class="background">
		<v-row align="center" justify="center">
			<v-col align="center" justify="center" cols="12">
				<v-card class="pa-3 mb-12" outlined width="600px">
					<v-card-subtitle align="left">
						Zadovoljavaju uvjete
					</v-card-subtitle>
					<v-card-text>
						<v-data-table
							:headers="zaglavlje"
							:items="zadovoljili"
							item-key="">
							<template v-slot:[`item.actions`]="{ item }">
								<v-icon dense @click="pogledajDetalje(item)">
									mdi-open-in-app
								</v-icon>
							</template>
						</v-data-table>
					</v-card-text>
				</v-card>
				<v-card class="pa-3" outlined width="600px">
					<v-card-subtitle align="left">
						Ne zadovoljavaju uvjete
					</v-card-subtitle>
					<v-card-text>
						<v-data-table
							:headers="zaglavlje"
							:items="nisuZadovoljili"
							item-key="">
							<template v-slot:[`item.actions`]="{ item }">
								<v-icon dense @click="pogledajDetalje(item)">
									mdi-open-in-app
								</v-icon>
							</template>
						</v-data-table>
					</v-card-text>
				</v-card>
			</v-col>
			<detalji
				v-if="detaljiVidljivi"
				:detalji="detaljiVidljivi"
				:student="student"
				@zatvoriFormu="zatvoriDetalje" />
		</v-row>
	</v-container>
</template>
<script>
import { zaglavlje } from "@/store.js";
import Detalji from "@/components/Detalji.vue";

export default {
	name: "drugi-zadatak",
	components: {
		Detalji,
	},
	data() {
		return {
			zadovoljili: [],
			nisuZadovoljili: [],
			sviStudenti: [],
			zaglavlje: zaglavlje,
			detaljiVidljivi: false,
			student: null,
		};
	},
	methods: {
		loadajStudente() {
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (studenti && studenti.length > 0) {
				this.sviStudenti = [...studenti];
			}
		},
		podijeliStudente() {
			if (this.sviStudenti && this.sviStudenti.length > 0) {
				debugger;
				this.zadovoljili = [
					...this.sviStudenti.filter((x) => x.brojDolazaka > 11),
				];
				this.nisuZadovoljili = [
					...this.sviStudenti.filter((x) => x.brojDolazaka < 10),
				];
			}
		},
		pogledajDetalje(student) {
			this.detaljiVidljivi = true;
			this.student = student;
		},
		zatvoriDetalje() {
			this.detaljiVidljivi = false;
		},
	},
	created() {
		this.loadajStudente();
		this.podijeliStudente();
	},
};
</script>
