## How I used data to find violators of U.N. sanctions against North Korea

By NICHOLAS DIAS

The North Korea regime continues to build and test nuclear bombs and missile systems that can reach South Korea and Japan. To no avail, numerous sanctions have been passed by the United Nations Security Council in an attempt to block Kim Jong-un and his predecessors from smuggling weapons, related materials and otherwise banned commodities in and out of the country.

Sanctions experts have largely attributed the U.N. sanction regime’s limited success to lax implementation on behalf of some of its member countries, which allows companies to violate sanctions with impunity. As one expert put it, “If 15 particular [U.N. countries] were serious to the max about enforcing the North Korea sanctions, the whole system would be in a good shape.”

Violators of a two sanctions resolutions can be identified computationally with a high degree of confidence: 

1. a resolution that ordered U.N. countries to prevent persons and companies registered in their countries from owning or providing almost any kind of service to vessels flying the North Korean flag, and
2. another that compelled the ship registries of U.N. countries to de-register any vessel operated by the Kim Jong-un regime. 

To this end, my analysis and reporting found that:

* 26 companies are violating U.N. sanctions by owning or providing services to ships flying the North Korean flag, according to data from IHS Markit. Of these companies, 14 are registered in Hong Kong. However, the list also includes companies in mainland China, the United Arab Emirates and Iraq.
* Almost half of the above companies appear to be linked to each another via two densely connected networks of UK shell companies that orbit addresses in Cardiff and London, respectively. All are joined to the network in various ways, including through apparent UK counterparts and shared directors and corporate secretaries.
* The North Korean-linked vessels flying the flags of U.N. countries saw dramatic shifts to other flag registries following the passage of the second resolution listed above. However, these ships did not return to the North Korean flag. Rather, they moved to the registries of other U.N. countries—namely Tanzania and Fiji. Then, suddenly, at the beginning of October, 34 DPRK-linked vessels under the Tanzanian registry moved to the ‘Unknown’ flagging category of IHS Markit’s records.
* Dozens of vessels that have been linked to the North Korean government were, as of February, listed under the ship registries of U.N. countries in potential violation of sanctions. The clear frontrunner of this group was Tanzania, who as of Oct. 2016 had 40 North Korean-linked vessels under its registry.
* Eight of the U.N. countries with ship registries flagging North Korean-linked vessels in potential violation of sanctions have neglected to provide written proof of sanctions implementation for half of the U.N. resolutions comprising the sanctions regime. Seven of them have been blacklisted by either the Paris or Tokyo MOUs, groups of port countries organized to enforce international maritime conventions.

The methodology below is split into two sections that correspond to these two resolutions. All tasks were performed using Python unless otherwise specified. Additional details about the choices I made in the course of programming can be found in the scripts themselves, which I’ve included in this repository.

**1 - Companies owning or providing services to North Korean-flagged vessels in violation of U.N. sanctions**

I began by downloading and parsing text records for all vessels that had ever used the North Korean flag—over 400. These documents were generated by IHS Markit, data supplier of the International Maritime Organization, and were accessed through LexisNexis. Importantly, the records contained the dates on which vessels changed flags, owners and managers.

I used Trifacta Wrangler to split the records between rows of a CSV, such that each row of the CSV corresponded to one document. Then, I processed the records to produce a table showing every registration, ownership and management period, and its start and end dates, for every vessel. This table allowed me to compare periods when vessels were flying the North Korean flag with the effective date of the resolution and produce a list of companies dealing with North Korean-flagged vessels in potential violation of U.N. sanctions.

Next, I wrote a scraper for the French Ministry of Transport’s Equasis website in order to pull the country in which each of my listed companies was located, as well as other information corroborating the IHS Markit records. The resulting table allowed me to produce a final list of sanctions violators.

After reporting on the companies my analysis had exposed, I discovered a number of links between my list of violators and what appeared to be shell companies in London and Cardiff. Suspecting that these shell companies may be connected to each other, I wrote another three scrapers for the UK’s Companies House website to pull each company’s address, directors and secretaries. The results of these scrapes were imported into Neo4j to model the connections between these companies, which facilitated the discovery of two networks of shell companies. One of these networks was directly linked to Ma Xiaohong, who is currently under investigation by FBI for helping North Korea evade U.S. sanctions. A visualization of one of the networks was made using Kumu and is included in this repository. 

**2 - Ship registries of U.N. countries failing to de-register vessels operated by the Kim Jong-un regime**

I used the same technique as before to collect and process IHS Markit records, creating tables of the flag histories of every vessel sanctioned by the U.N. or linked to the North Korean government via ownership or trade routes by Leo Byrne of NK News. Byrne’s list of vessels was confirmed to be generally reliable by a member of the U.N. panel of experts that monitors the North Korean sanctions regime.

Again, I compared flag registration periods with the effective date of the relevant resolution, as well as a list of U.N. countries. One result was a table of tentative illegal flagging periods by country, i.e., the number of instances where the ship registry of a country may have flagged a North Korean-linked vessel after the resolution date. Another was the list of vessels that appeared to be currently flagged by U.N. countries in violation of sanctions.

The current flag of every vessel suspected to be flagged illegally was scraped from Equasis to corroborate the IHS Markit records, resulting in a final tally of illegal flaggings for the ship registries of several U.N. countries.

Additionally, I wrote an algorithm that converted the tables I generated from the IHS Markit records into a count table showing how many vessels were using each flag for every day of the past year. I fed the data from this last table into Infogr.am to create an area chart, which is included in this repository. 