**OSM2GMNS: A tool for generating GMNS standard data file**

**from OpenStreet Map**

**Version 0.9**

OpenStreet Map (OSM) is a free, crowdsourced, worldwide mapping project
and geospatial data repository. This user guide describes a data
conversion tool of OMS2GMNS based on OSMnx, to directly download the OSM
map data and then generate node and link network file in the GMNS
format. For more information, you can visit OpenStreet Map website at
<https://www.openstreetmap.org/>, and check out the latest development
about OSMnx at <https://geoffboeing.com/.>

**1. Understanding GMNS**

GMNS(General Travel Network Format Specification), proposed by the
Zephyr Foundation, which aims to advance the field through flexible and
efficient support, education, guidance, encouragement, and incubation.
Further details can be found at
https://zephyrtransport.org/projects/2-network-standard-and-tools/

A transportation network in GMNS format typically includes node.csv and
link.csv files, as shown in the following table.

node.csv:

  --------- --------- ---------- ----------- -----------
  name      node_id   zone_id    ctrl_type   node_type
  x_coord   y_coord   geometry               
  --------- --------- ---------- ----------- -----------

link.csv:

  -------- ---------- -------------- ------------ -----------
  name     link_id    from_node_id   to_node_id   dir_flag
  length   lanes      free_speed     capacity     link_type
           geometry                               
  -------- ---------- -------------- ------------ -----------

A list of typical link types from OSM includes the following.

  ----------- ----------------
  link_type   link_type_name
  1           motorway
  2           trunk
  3           primary
  4           secondary
  5           tertiary
  6           residential
  7           others
  ----------- ----------------

**2.How to install OSMnx?**

Further details about OSMnx can be found:
<https://geoffboeing.com/2016/11/osmnx-python-street-networks/>.

Step 1: Set a new virtual environment in Anaconda 3 with Python 3.7

![](media/image1.png){width="5.774305555555555in"
height="3.073611111111111in"}

Step 2: Open Terminal in this virtual environment, and install 3
packages namely rtree, gdal, fional in sequence. Input the command line
in terminal: *pip install XXXX.whl*, while the specific versions as
recommended as follows:

![](media/image2.png){width="2.45in" height="0.51875in"}

![](media/image3.png){width="5.759722222222222in"
height="3.0506944444444444in"}

Step 3: Install OSMnx, Type a command line: *pip install osmnx*

![](media/image4.png){width="5.763194444444444in"
height="0.6819444444444445in"}

Step 4: Open the Python IDE such as Pycharm for a typical configuration.

**3.How to use OSM2GMNS?**

We will use the city of Tempe as an example to illustrate how to use
OSM2GMNS tool.

**Step 1: Determining the research boundary of the map**

For example, we want to obtain the map data of Tempe campus of ASU, with
a boundary shown in the map below.

First, please adjust the map to the location of interest:

![](media/image5.png){width="5.777083333333334in"
height="2.754861111111111in"}

Second, click on the "export" button:

![](media/image6.png){width="5.777083333333334in"
height="2.7576388888888888in"}

Then, we can obtain the latitude and longitude coordinate range on the
left side of the window. Please take a note about 4 coordinate values.
In this example, the four values are 33.4135, 33.4235, -111.9216, and
-111.9416, to be used as the input for bbox in the Python code.

**Step 2: Determining the parameters of the *map crawler***

Go to the Python environment and modify the bbox parameter as bbox =
\[33.4135, 33.4235, -111.9216, -111.9416\] in the codes.

Remarks:

\(1\) G = ox.graph_from_bbox(\*bbox, network_type=\'all\'): \'drive\'
means that we only obtain vehicle road, and \'all\' means that we can
obtain all types of roads.

(2) attributes = ox.graph_to_gdfs(G, edges=False): edges=False means
    that no link data will be obtained. Similarly, nodes=False means
    that no node data will be obtained.

**Step 3: Running the OSM2GMNS Python code**

**Step 4: Outputting files**

There are three output files, namely node.csv, link.csv, and demand.csv
from the OSM2GMNS package. The node and link attributes are saved in
node.csv and link.csv respectively, while the O-D demand file is
automatically generated with default values.

**Step 5: Visualization in NEXTA**

You can open the Traffic network project(node.csv) with NEXTA and then
the downloaded map data can be visualized with GMNS format(node.csv,
link.csv).

![](media/image7.png){width="4.0152777777777775in"
height="2.4069444444444446in"}

![](media/image8.png){width="5.759722222222222in"
height="3.0541666666666667in"}
