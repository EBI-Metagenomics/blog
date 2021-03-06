---
published: true
category: tools
emg:
  text: MGnify REST API
  url: >-
    https://www.ebi.ac.uk/metagenomics/api/
layout: post
---
![Python script]({{site.baseurl}}/assets/media/images/posts/ico_code_EMG_grey.png)
Want to perform comprehensive meta-analysis of samples from publicly available metagenomics studies? Interested in discovering patterns in metagenomic data to predict disease? Our REST API allows both human and machines to query over 100,000 publicly available metagenomic and metatranscriptomic datasets. The base URL to the API [https://www.ebi.ac.uk/metagenomics/api/](https://www.ebi.ac.uk/metagenomics/api/) provides access to several data collections, such as studies, samples, runs, biomes and experiment-types. They can be filtered by a set of attributes, such as biome, allowing selection of samples that belong to the same microbial ecosystem. For instance, to retrieve oceanic data: [https://www.ebi.ac.uk/metagenomics/api/latest/studies?lineage=root:Environmental:Aquatic:Marine:Oceanic](https://www.ebi.ac.uk/metagenomics/api/latest/studies?lineage=root:Environmental:Aquatic:Marine:Oceanic). Retrieving data from our API is as simple as sending an HTTP request, where the response returns a JSON object formatted data structure that contains the resource type, associated object identifier (id) with attributes and relationships linking to other resources. For example, [https://www.ebi.ac.uk/metagenomics/api/latest/studies/PRJEB1787](https://www.ebi.ac.uk/metagenomics/api/latest/studies/PRJEB1787) retrieves a metagenomics dataset produced during experiments of the Tara Oceans Expedition.

    curl -X GET -H "Accept: application/json" "https://www.ebi.ac.uk/metagenomics/api/latest/studies/PRJEB1787"

    Content-Type: application/vnd.api+json

    {
        "data": {
            "type": "studies",
            "id": "MGYS00000410",
            "attributes": {
                "samples-count": 136,
                "accession": "MGYS00000410",
                "bioproject": "PRJEB1787",
                "secondary-accession": "ERP001736",
                "centre-name": "GSC",
                "public-release-date": null,
                "study-abstract": "Seawater was filtered from different depths to retain small cell sizes (Bacteria Organisms). The DNA was extracted and submitted to high throughput sequencing.",
                "study-name": "Shotgun Sequencing of Tara Oceans DNA samples corresponding to size fractions for  prokaryotes.",
                "data-origination": "SUBMITTED",
                "last-update": "2016-01-20T14:12:06"
            },
            "relationships": {
                "geocoordinates": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/geocoordinates"
                    }
                },
                "analyses": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/analyses"
                    }
                },
                "biomes": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/biomes"
                    },
                    "meta": {
                        "count": 1
                    },
                    "data": [
                        {
                            "type": "biomes",
                            "id": "root:Environmental:Aquatic:Marine:Oceanic",
                            "links": {
                                "self": "https://www.ebi.ac.uk/metagenomics/api/v1/biomes/root:Environmental:Aquatic:Marine:Oceanic"
                            }
                        }
                    ]
                },
                "studies": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/studies"
                    },
                    "meta": {
                        "count": 1
                    },
                    "data": [
                        {
                            "type": "studies",
                            "id": "MGYS00002008",
                            "links": {
                                "self": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00002008"
                            }
                        }
                    ]
                },
                "downloads": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/downloads"
                    }
                },
                "samples": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/samples"
                    }
                },
                "publications": {
                    "links": {
                        "related": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410/publications"
                    }
                }
            },
            "links": {
                "self": "https://www.ebi.ac.uk/metagenomics/api/v1/studies/MGYS00000410"
            }
        }
    }

or using 3rd party Python client jsonapi-client and pandas to export data to CSV (the following example is compatible with Python 3.6 only):

    from pandas import DataFrame
    from jsonapi_client import Session, Filter
    
    API_BASE = 'https://www.ebi.ac.uk/metagenomics/api/latest/'

    with Session(API_BASE) as s:
        df = DataFrame(
            columns=
                ('sample_name', 'biome', 'feature', 'material', 'longitude', 'latitude')
        )
        df.index.name = 'accession'

        params = {
            'study_accession': 'PRJEB1787',
            'page_size': 100,
        }
        f = Filter(params)
        for sample in s.iterate('samples', f):
            df.loc[sample.accession] = [
                sample.sample_name,
                sample.environment_biome,
                sample.environment_feature,
                sample.environment_material,
                sample.longitude,
                sample.latitude,
            ]
    df.to_csv('output.csv')

For more examples, try our sample Jupyter notebook [https://github.com/EBI-metagenomics/emgapi-examples/blob/master/emgapi/examples/notebook/answers/ANSWER_examples.ipynb](https://github.com/EBI-metagenomics/emgapi-examples/blob/master/emgapi/examples/notebook/answers/ANSWER_examples.ipynb)

Our API is documented using interactive HTML interface to visualise and simplify interaction with our resources. Detailed explanations of the functionality of all resources, along with many examples, are available on [https://www.ebi.ac.uk/metagenomics/api/docs/](https://www.ebi.ac.uk/metagenomics/api/docs/).

Happy clicking!
