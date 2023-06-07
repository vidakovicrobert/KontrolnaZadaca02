<template>
	<v-sheet color="white" elevation="1" height="auto" outlined width="600px">
		<v-container fill-height fluid class="background">
			<v-row>
				<v-col cols="12">
					<v-card class="pa-3" outlined width="600px">
						<v-card-title>Dodaj studenta</v-card-title>
						<v-card-text>
							<v-form @input="checkFormValidity" v-model="valid">
								<v-text-field v-model="ime" dense label="Ime" clearable type="text" outlined required>
								</v-text-field>
								<v-text-field v-model="prezime" dense label="Prezime" clearable outlined required>
								</v-text-field>
								<v-text-field v-model="brojDolazaka" dense label="Broj dolazaka(maksimalno 15)" clearable
									outlined required>
								</v-text-field>
								<v-text-field v-model="prviKolokvij" dense
									label="Rezultat drugog kolokvija (maksimalno 40 bodova)" clearable outlined required>
								</v-text-field>
								<v-text-field v-model="drugiKolokvij" dense
									label="Rezultat drugog kolokvija (maksimalno 40 bodova)" clearable outlined required>
								</v-text-field>
								<v-text-field v-model="kontinuiranoPracenje" dense
									label="Kontinuirano praćenje (maksimalno 20 bodova)" clearable outlined required>
								</v-text-field>
							</v-form>
						</v-card-text>
						<v-card-actions>
							<v-btn color="black" class="white--text" elevation="0" @click="obrisiSveUnesenePodatke">
								BRISI PODATKE
							</v-btn>

							<v-spacer></v-spacer>
							<v-btn color="red" class="red--text" outlined elevation="0" @click="ocistiFormu">
								OČISTI
							</v-btn>
							<v-btn color="gray" class="gray--text" outlined elevation="0" @click="dodajStudenta"
								:disabled="!valid">
								OK
							</v-btn>
						</v-card-actions>
					</v-card>
				</v-col>
			</v-row>
		</v-container>
	</v-sheet>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
			ime: " ",
			prezime: "",
			brojDolazaka: "",
			prviKolokvij: "",
			drugiKolokvij: "",
			kontinuiranoPracenje: "",
			valid: false,
		};
	},
	watch: {},
	methods: {
		ocistiFormu() {
			this.ime = "";
			this.prezime = "";
			this.brojDolazaka = "";
			this.prviKolokvij = "";
			this.drugiKolokvij = "";
			this.kontinuiranoPracenje = "";
			this.valid = false;
		},
		dodajStudenta() {
			let noviStudent = {
				//Dodaj propertyje
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
		checkFormValidity() {
			this.valid =
				this.ime && this.prezime && this.brojDolazaka && this.prviKolokvij && this.drugiKolokvij && this.kontinuiranoPracenje;
		},

	},
};
</script>
