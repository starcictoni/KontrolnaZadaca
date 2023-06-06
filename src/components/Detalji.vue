<template>
	<v-dialog v-model="detalji" width="400" height="600">
		<v-container>
			<v-row class="text-center">
				<v-col cols="12" class="pa-0">
					<v-card outlined class="pa-3">
						<v-card-title>Nije zadovoljio je uvjete</v-card-title>
						<v-card-text>
							<v-text-field
								v-model="ime"
								disabled
								dense
								label="Ime"
								clearble
								type="text"
								outlined></v-text-field>
							<v-text-field
								v-model="prezime"
								color="red"
								disabled
								dense
								label="Prezime"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="brojDolazaka"
								disabled
								dense
								label="Broj dolazaka (maksimalno 15)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="prviKolokvij"
								disabled
								dense
								label="Rezultat prvog kolokvija (maksimalno 40 bodova)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="drugiKolokvij"
								disabled
								dense
								label="Rezultat drugog kolokvija (maksimalno 40 bodova)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="kontinuiranoPracenje"
								disabled
								dense
								label="Kontinuirano pracenje (maksimalno 20 bodova)"
								clearble
								outlined></v-text-field>
						</v-card-text>
						<v-card-actions>
							<v-spacer></v-spacer>
							<v-btn @click="zatvoriFormu" color="red" outlined>
								ZATVORI
							</v-btn>
						</v-card-actions>
					</v-card>
				</v-col>
			</v-row>
		</v-container>
	</v-dialog>
</template>
<script>
export default {
	name: "Detalji",
	props: ["detalji", "student"],
	data() {
		return {
			width: 300,
			height: 400,
			image: null,
			taskDescription: null,
			ime: null,
			prezime: null,
			brojDolazaka: null,
			prviKolokvij: null,
			drugiKolokvij: null,
			kontinuiranoPracenje: null,
		};
	},
	methods: {
		zatvoriFormu() {
			this.$emit("zatvoriFormu", false);
		},
		popuniPolja() {
			this.ime = this.student.ime;
			this.prezime = this.student.prezime;
			this.brojDolazaka = this.student.brojDolazaka;
			this.prviKolokvij = this.student.prviKolokvij;
			this.drugiKolokvij = this.student.drugiKolokvij;
			this.kontinuiranoPracenje = this.student.kontinuiranoPracenje;
		},
	},
	created() {
		this.popuniPolja();
	},
};
</script>
