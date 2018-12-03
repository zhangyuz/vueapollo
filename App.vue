<template>
	<div id="app">
	  <v-app>
		  <template>
				<v-layout row>
					<v-flex xs12 sm6 offset-sm3>
						<v-card>
							<v-toolbar dark>
							  <v-select
								  :autocomplete="true"
									:items="availableCurrencies"
									v-model="selectedCurrency"
									:item-text="'id'"
									:item-value="'id'"
									:loading="loadingRates"
									label="Select currency"
									dark
								></v-select>
							</v-toolbar>
							<v-list two-line dark>
								<template v-for="rate in rates.rates">
								  <v-list-tile>
									  <v-list-tile-content>
											<v-list-tile-title v-html="rate.currency"></v-list-tile-title>
										</v-list-tile-content>
										<v-list-tile-action>
											<v-list-tile-title v-html="rate.rate"></v-list-tile-title>
										</v-list-tile-action>
									</v-list-tile>
								</template>
							</v-list>
						</v-card>
					</v-flex>
				</v-layout>
			</template>
	  </v-app>
	</div>
</template>

<script>
  import { AVAILABLE_CURRENCIES_QUERY, RATES_QUERY } from './graphql'

	export default {
    name: 'app',
		data () {
			return {
				availableCurrencies: [],
				loading: 0,
				rates: [],
				selectedCurrency: 'USD'
			}
		},
		computed: {
			loadingRates () {
        return !!this.loading
			}
		},
		apollo: {
			$loadingKey: 'loading',
			availableCurrencies: {
				query: AVAILABLE_CURRENCIES_QUERY
			},
			rates: {
				query: RATES_QUERY,
				variables () {
					return {
						currency: this.selectedCurrency
					}
				}
			}
		}
  }
</script>
