# Tradesman Demo

This is a simple Tradesman demo project presented at the 2023 TRB Innovations in Travel Modelling conference in Indianapolis, Indiana USA between June 3rd and June 6th.

It consists of a single Jupyter Notebook that has been tested with Python 3.10 running on Windows 11 and on *Google Colab*

Our [webpage for this conference(http://itm2023.outerloop.io) contains references to all resources presented at ITM 2023.

## Running on Windows

The setup below assumes you have Python and Windows Terminal installed.

On Windows Terminal:

    git clone https://github.com/outerl/tradesman-demo.git
    cd tradesman-demo

    python -m pip install virtualenv

    python -m virtualenv .venv
    .\.venv\Scripts\activate.ps1

    python -m install -r requirements.txt
    jupyter lab


## Running on Google Colab

You can just jump straight into Google Colab to run this tutorial notebook in the cloud.

<a href="https://colab.research.google.com/github/outerl/tradesman-demo/blob/main/model_building_example.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab"/></a>

Please note that, when using the free version of Google Colab, you are not guaranteed to run the entire notebook before shutting down.


## Indiana example

For those interested in looking at the results of a more substantial example, a sample model for Indiananapolis was also prepared and is available for [DOWNLOAD](https://itm2023.s3.amazonaws.com/LongAn_base_model.zip).

The Indianapolis example provided in the tutorial was generated on 30/05/2023 with the code below

    import os
    os.environ['USE_PYGEOS'] = '0'

    from uuid import uuid4
    from tradesman.model import Tradesman
    from tempfile import gettempdir

    model_place = "Indianapolis, Indiana USA"
    folder = os.path.join(gettempdir(), "Indianapolis")
    
    model = Tradesman(network_path=folder, model_place=model_place)

    model.import_model_area()
    model.add_country_borders()
    model.import_subdivisions(subdivision_levels=2, overwrite=True)
    model.import_network()
    model.import_population()
    model.build_zoning(hexbin_size=200, min_zone_pop=250, max_zone_pop=2000)
    model.import_pop_by_sex_and_age()
    model.import_amenities()
    model.import_buildings(download_from_bing=False)
    model.build_population_synthesizer_data(sample_size=0.02)
    model.synthesize_population()