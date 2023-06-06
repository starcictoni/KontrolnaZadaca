<template>
	<v-container fill-height fluid class="background">
		<v-row align="center" justify="center">
			<v-col align="center" justify="center" cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Dodaj studenta</v-card-title>
					<v-card-text>
						<v-form v-model="valid">
							<v-text-field
								v-model="ime"
								:rules="[rules.required]"
								dense
								label="Ime"
								clearble
								type="text"
								outlined></v-text-field>
							<v-text-field
								v-model="prezime"
								:rules="[rules.required]"
								dense
								label="Prezime"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="brojDolazaka"
								:rules="[rules.required, rules.maxFifteen]"
								dense
								label="Broj dolazaka (maksimalno 15)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="prviKolokvij"
								:rules="[rules.required, rules.maxForty]"
								dense
								label="Rezultat prvog kolokvija (maksimalno 40 bodova)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="drugiKolokvij"
								:rules="[rules.required, rules.maxForty]"
								dense
								label="Rezultat drugog kolokvija (maksimalno 40 bodova)"
								clearble
								outlined></v-text-field>
							<v-text-field
								v-model="kontinuiranoPracenje"
								:rules="[rules.required, rules.maxTwenty]"
								dense
								label="Kontinuirano pracenje (maksimalno 20 bodova)"
								clearble
								outlined></v-text-field>
						</v-form>
					</v-card-text>
					<v-card-actions>
						<v-btn
							color="black"
							class="white--text"
							elevation="0"
							@click="obrisiSveUnesenePodatke">
							BRISI PODATKE
						</v-btn>
						<v-spacer></v-spacer>
						<v-btn @click="ocistiFormu" color="red" outlined>
							OČISTI
						</v-btn>
						<v-btn
							:disabled="jeLiButtonDisabled"
							@click="dodajStudenta"
							outlined>
							OK
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
			ime: "",
			prezime: "",
			//od 0 do 15
			brojDolazaka: null,
			//od 0 do 40
			prviKolokvij: null,
			//od 0 do 40
			drugiKolokvij: null,
			//od 0 do 20
			kontinuiranoPracenje: null,
			valid: true,
			jeLiButtonDisabled: true,
			rules: {
				required: (value) => {
					return !!value || "Required.";
				},
				maxForty: (value) => {
					if (value > 40 || value < 0) {
						return "Not valid.";
					} else {
						return true;
					}
				},
				maxTwenty: (value) => {
					if (value > 20 || value < 0) {
						return "Not valid.";
					} else {
						return true;
					}
				},
				maxFifteen: (value) => {
					if (value > 15 || value < 0) {
						return "Not valid.";
					} else {
						return true;
					}
				},
			},
		};
	},
	watch: {
		valid: function (newVal, oldVal) {
			debugger;
			if (newVal != true) {
				this.jeLiButtonDisabled = true;
			} else {
				this.jeLiButtonDisabled = false;
			}
		},
	},
	methods: {
		ocistiFormu() {
			this.ime = null;
			this.prezime = null;
			this.brojDolazaka = null;
			this.prviKolokvij = null;
			this.drugiKolokvij = null;
			this.kontinuiranoPracenje = null;
		},
		dodajStudenta() {
			let noviStudent = {
				ime: this.ime,
				prezime: this.prezime,
				brojDolazaka: this.brojDolazaka,
				prviKolokvij: this.prviKolokvij,
				drugiKolokvij: this.drugiKolokvij,
				kontinuiranoPracenje: this.kontinuiranoPracenje,
			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},
	},
};
</script>
