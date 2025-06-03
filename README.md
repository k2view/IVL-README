# IVL-README
# Table of Contents 

[Description](#description)

- [Investigator Categories](#investigator-categories)

[Installation](#installation)

- [Requirements](#requirements)

- [Step 1: Download the Investigator Library
](#step-1-download-the-investigator-library)

- [Step 2: Validate Library Components](#step-2-validate-library-components)

- [Step 4: Configure And Validate Interfaces](#step-4-configure-and-validate-interfaces)

- [Step 5: Integrate IID Consumer into Cloud Space](#step-5-integrate-iid-consumer-into-cloud-space)

- [Step 6: Deploy Added/Updated Logical Units](#step-6-deploy-addedupdated-logical-units)

[How To Use](#how-to-use)

- [*IID Search page*](#iid-search-page)

- [*Kafka Topics page*](#kafka-topics-page)

- [*IID Consumer page*](#iid-consumer-page)

# 

# Description

The **Investigator Library** is a Fabric-based application designed to
streamline investigations and enhance efficiency. It analyzes data from
Logical Unit Instances (LUIs), Kafka topics, and monitors active
consumers, providing real-time and summary data on the **Investigator
Web Page**.

## Investigator Categories

The library includes three primary categories:

1.  **IID Search**

    Used for instance-specific investigations.

    > Mandatory inputs:

    - LU Type

    - IID

    > Optional inputs:

    - Sub categories- check box with 4 options: System DB, LUi Data, Delta
    Topics, Log

    <table>
    <colgroup>
    <col style="width: 17%" />
    <col style="width: 82%" />
    </colgroup>
    <thead>
    <tr>
    <th>Tab</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <th>System DB</th>
    <td><p>Displays instance data from the System DB.</p>
    <ol type="1">
    <li><p>Entity info</p></li>
    <li><p>Batch info</p></li>
    <li><p>Stats info</p></li>
    <li><p>IIDFinder staging info</p></li>
    </ol></td>
    </tr>
    <tr>
    <th>LUi Data</th>
    <td>Displays all the instance table data stored in Fabric.</td>
    </tr>
    <tr>
    <th>Delta Topics</th>
    <td>Displays delta messages for this instance in the LU delta
    topic.</td>
    </tr>
    <tr>
    <th>Log</th>
    <td>Displays K2Fabric log messages for GET executions of the selected
    instance within a specified time range.</td>
    </tr>
    </tbody>
    </table>

2.  **Kafka Topics**

    Supports Kafka/IDFinder-related investigations.

    <table>
    <colgroup>
    <col style="width: 17%" />
    <col style="width: 82%" />
    </colgroup>
    <thead>
    <tr>
    <th>Tab</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <th>Messages</th>
    <td><p>Displays Kafka topic data based on user inputs.</p>
    <p>Mandatory Inputs:</p>
    <p>Search Type (Delta/IIDFinder)</p>
    <p>Topic</p>
    <p>Advanced/Optional Inputs:</p>
    <ol type="1">
    <li><p>Partition (Specify the topic partition, default is to fetch from
    all partitions)</p></li>
    <li><p>Offset (Specify the message offset, default is from
    beginning)</p></li>
    <li><p>Limit (Set the maximum number of returned messages; default is
    <strong>1000</strong>, adjustable within the range <strong>[1,
    10,000]</strong>)</p></li>
    <li><p>Regex (filters messages containing given value)</p></li>
    <li><p>Operation Type (Kafka message operation
    type-insert/update/delete)</p></li>
    <li><p>Date Range (Time range of the messages to be displayed)</p></li>
    </ol>
    <p>Based on these inputs, the library searches and analyzes messages
    from the Kafka topics, utilizing the specified filtering
    parameters.</p></td>
    </tr>
    <tr>
    <th>Lag</th>
    <td><p>Displays Kafka topics lag data based on user inputs.</p>
    <p>Mandatory Inputs:</p>
    <ol type="1">
    <li><p>Search Type (Delta/IIDFinder)</p></li>
    </ol>
    <p>Advanced/Optional Inputs:</p>
    <ol start="2" type="1">
    <li><p>Topic</p></li>
    </ol>
    <p>Output:</p>
    <ul>
    <li><p>No topic name is provided:</p></li>
    </ul>
    <ol type="1">
    <li><p>Total group lag across all topics.</p></li>
    <li><p>Lag for each topic in the group.</p></li>
    <li><p>An option to expand and view topic details by clicking
    <strong>"Show Details"</strong>.</p></li>
    </ol>
    <ul>
    <li><p>Topic name provided:</p></li>
    </ul>
    <ol type="1">
    <li><p>Total Lag for chosen topic</p></li>
    <li><p>Lag per Partition</p></li>
    <li><p>CurrOffset (Current Offset) per Partition</p></li>
    <li><p>EndOffset (End Offset) per Partition</p></li>
    </ol></td>
    </tr>
    </tbody>
    </table>

3.  **IID Consumer**

    Tracks and summarizes consumer activity defined in the **mtLUTopic**
    MTable**.**

    <table>
    <colgroup>
    <col style="width: 17%" />
    <col style="width: 82%" />
    </colgroup>
    <thead>
    <tr>
    <th>Tab</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <th>Summary</th>
    <td><p>Provides overall statistics for each subscribed topic by the IID
    Consumers.</p>
    <p>Mandatory inputs:</p>
    <ol type="1">
    <li><p>LU Type – The Logical Unit of the IID Consumer for which
    statistics are displayed.</p></li>
    <li><p>Time Window – The time range for collecting statistics (default:
    60 minutes).</p></li>
    </ol>
    <p>The main table output presents a Kafka summary for each topic.</p>
    <p>Output:</p>
    <p>Lu type</p>
    <p>Topic</p>
    <p>Group</p>
    <p>Partition count</p>
    <p>Lag- topic’s lag</p>
    <p>Max partition backlog – partition with largest lag (for partition 0
    with lag of 20: 0(20))</p>
    <p>Total count – the number of consumed messages</p>
    <p>Failure count – the number of failed messages</p>
    <p>An option to expand and view topic details by clicking <strong>"Show
    Details"</strong>.</p>
    <p><strong>"Show Details"</strong> reveals a detailed breakdown of the
    partition data for the corresponding topic:</p>
    <ol type="1">
    <li><p>Partition – Topic's partition</p></li>
    <li><p>Lag – Partition's lag</p></li>
    <li><p>Node id – the node on which the partition's consumer job
    ran</p></li>
    <li><p>Job uid – the uid of the consumer job</p></li>
    <li><p>Total count – the number of consumed messages</p></li>
    <li><p>Failure count – the number of failed messages</p></li>
    </ol></td>
    </tr>
    <tr>
    <th>Current</th>
    <td><p>Displays real-time data on all actively consumed messages from
    running consumers listed in the <strong>MTable</strong>.</p>
    <p>The following details are provided:</p>
    <ol type="1">
    <li><p>LU Type – Logical Unit associated with the consumer</p></li>
    <li><p>IID – Instance ID extracted from the currently processed
    message</p></li>
    <li><p>Topic – Kafka topic from which the consumer is retrieving
    messages</p></li>
    <li><p>Partition – Partition of the topic being consumed</p></li>
    <li><p>Offset – Offset of the message within the Kafka topic</p></li>
    <li><p>Status – Current processing state (SYNC_IN_PROCESS /
    PROCESSING_MESSAGE)</p></li>
    <li><p>Duration – Time elapsed during message processing</p></li>
    <li><p>Start Time – Timestamp indicating when message processing
    began</p></li>
    <li><p>Job Name – Name of the consumer job</p></li>
    <li><p>Node – Node where the consumer job is running</p></li>
    </ol>
    <p><strong>Auto Refresh Feature:</strong></p>
    <ul>
    <li><p>When enabled, the table refreshes every 5 seconds, ensuring
    real-time monitoring of active consumers.</p></li>
    </ul></td>
    </tr>
    <tr>
    <th>History</th>
    <td><p>Provides a comprehensive record of IID consumer statistics,
    allowing users to review past message processing details.</p>
    <p>Mandatory Inputs:</p>
    <ol type="1">
    <li><p>LU Type – The Logical Unit where the consumer exists</p></li>
    <li><p>Topic – The Kafka topic from which the consumer retrieves
    messages</p></li>
    <li><p>Start Time – The start time for data retrieval</p></li>
    </ol>
    <p>Advanced/Optional Inputs:</p>
    <ol type="1">
    <li><p>End Time – The end time for the historical data
    retrieval</p></li>
    <li><p>Partition – The Kafka topic partition</p></li>
    </ol>
    <p>Additional filtering can be added through search on the entire table
    or by column.</p>
    <p>The table includes the following information:</p>
    <ol type="1">
    <li><p>IID – Instance ID</p></li>
    <li><p>Start Time – Timestamp indicating when message process
    started</p></li>
    <li><p>End Time – Timestamp indicating when message process
    ended</p></li>
    <li><p>Status – Message state (PROCCESSED/SKIPPED/FAILED)</p></li>
    <li><p>Process Duration – Time elapsed during process</p></li>
    <li><p>Sync Duration – Time elapsed during sync</p></li>
    <li><p>Partition – Topic's partition</p></li>
    <li><p>Node ID – The node on which the partition's consumer job
    ran</p></li>
    <li><p>UID – The UID of the consumer job</p></li>
    <li><p>Offset – Offset of the message within the Kafka topic</p></li>
    <li><p>Error – Error message (if applicable, for failed
    processes)</p></li>
    <li><p>Topic – Kafka topic from which the consumer is retrieving
    messages</p></li>
    </ol>
    <p>Limitations:</p>
    <p>-Time window is restricted to <strong>500</strong> hours, if you
    choose a larger time window the massage: “The selected time window
    exceeds the acceptable range” will appear.</p></td>
    </tr>
    </tbody>
    </table>

# Installation

## Requirements

- **Fabric Version**: 8.2 or higher

## Step 1: Download the Investigator Library

1.  Click on Extensions GUI on the left side of your studio’s screen:

    <img src="media/image1.png"
    style="width:3.66718in;height:4.21934in" />

2.  Search for the “Investigator” extension and click Install.

## Step 2: Validate Library Components

The following components will be integrated into your workspace:

1.  Logical Unit: **Investigator**

2.  Interfaces:  
    **a. dbCassandraIVL  
    b. IVL_IIDF_KAFKA  
    c. IVL_DELTA_KAFKA**

3.  JAR file: **json-20231013.jar** under /lib

4.  Logic Folder: **Investigator** under /Web Services:

5.  A new application added to Application window called "Investigator"

## Step 4: Configure And Validate Interfaces

#### **Configure Connection Parameters:**

#### **dbCassandraIVL:**

- Host – Cassandra host of your cloud environment

- Port – Cassandra port of your cloud environnement

- User – Cassandra user credentials

- Password – Cassandra authentication password

> Configure any additional parameters required to establish a connection
> to the Cassandra instance.

2.  **IVL_IIDF_KAFKA:**

- **Bootstrap Servers**: IDFinder Kafka bootstrap server

- **Group ID**: Investigator

- **Data Type**: String

> Configure any additional parameters required to establish a connection
> to the IDFinder Kafka instance.

3.  **IVL_DELTA_KAFKA:**

- **Bootstrap Servers**: Internal Kafka bootstrap server

- **Group ID**: Investigator

- **Data Type**: Long

> Configure any additional parameters required to establish a connection
> to the Internal Kafka instance.

### ***Validate Interfaces Connectivity:***

In the interface, click **Test Connection** to ensure the connection is
functioning as expected.

Testing the connection verifies the connectivity between Fabric and the
Cassandra\\ KAFKA services, ensuring successful integration.

## <img src="media/image2.png" style="width:5.63389in;height:3.16545in" />

## Step 5: Integrate IID Consumer into Cloud Space

#### **Configure the Investigator IID Consumer MTable:**

1.  Edit mtLUTopic Mtable:

    1.  Navigate to the MTable Folder within the Investigator LU

    2.  Open mtLUTopic.csv
    
    <img src="media/image3.png" style="width:2.92513in;height:1.90587in" />

3.  For each IID Consumer in your project, add a row in the MTable with
    the following details:

    1.  LU_TYPE – The Logical Unit where the consumer exists

    2.  INTERFACE_NAME – The Kafka interface used to fetch Kafka
        consumer details

    3.  TOPIC_NAME – The Kafka topic the consumer subscribes to

    4.  GROUP_NAME – The Kafka consumer group

    5.  JOB_NAME – The consumer job name, formatted as LuName.JobName

    6.  DESCRIPTION – A brief description of the consumer job

    <img src="media/image4.png" style="width:5.60031in;height:1.05305in" />

#### **Integrate Consumer Stats Write Actors in the Broadway Consumer:**

The Investigator Library includes two key actors responsible for writing
statistics related to the **IID Consumer**. These actors must be
integrated into consumer jobs at various stages to track the consumption
progress. For example, they should be added at **message handling
start**, **GET execution**, and **processing completion**.

1.  **ivlConsumerCurrentStatsWrite**

    This actor is used for the **"Current"** tab on the IID Consumer page.
    It records real-time statistics of messages being processed by the IID
    Consumer at different stages of consumption.

    **Required Inputs for Each Stage:**

    - **lutype** – Logical Unit type of the consumer

    <!-- -->

    - **topic** – Kafka topic the consumer is consuming from

    - **partition** – The partition of the Kafka topic that the consumer
    subscribes to

    - **node** – The node on which the consumer job is running

    - **jobname** – The name of the consumer job

    - **IID** – The Instance ID of the processing message

    - **startTime** – The timestamp when message processing started

    - **status** – The status of the message handling (e.g., SYNC_IN_PROCESS
    / PROCESSING_MESSAGE)

    - **offset** – The offset of the message in the Kafka topic

2.  **ivlConsumerStatsWrite**

    This actor is used for the **"Summary/History"** tab on the IID Consumer
    page. It records statistics of messages that have been processed by the
    IID Consumer at different stages of consumption.

    **Required Inputs for Each Stage:**

    - **iid** – Instance ID of the processed message

    <!-- -->

    - **uid** – UID of the consumer job

    - **start_time** – Timestamp when message processing started

    - **end_time** – Timestamp when message processing ended

    - **process_duration** – Time taken to process the message

    - **status** – Processing status (e.g., PROCESSED, SKIPPED, FAILED,
    COMPLETED)

    - **error** – Error message (if any) encountered during processing

    - **offset** – Offset of the message in the Kafka topic

    - **partition** – The partition of the Kafka topic that the consumer
    subscribes to

    - **sync_duration** – Time taken to synchronize and handle the message

    - **topic** – Kafka topic the consumer is consuming from

    - **time_window** – The time range for processing messages. Format time
    to: yyyyMMddHH

    - **group_id** – Identifier for the Kafka consumer group.

    - **node_id** – The node on which the consumer job was executed.

    > This integration ensures that all consumer activities are logged,
    > allowing the Investigator Library to effectively track and monitor
    > consumers through the IID Consumer page.

    **Note:**

    > In the IIDFinder Library, these actors are already integrated into the
    > Delta Consumer. Therefore, if the IIDFinder Library is installed in
    > your cloud space, they should be removed from the IVL Library to
    > prevent duplication.

#### **Consumer Stats Globals:**

- IVL_SKIPPED_IIDS_STATS: If set to true, logs of skipped IIDs
  gets are recorded in the IID Consumer detailed_stats table.

- IVL_STATS_ACTIVE: If set to true, IID Consumer stats are
  logged to the detailed_stats table and current stats MTable.

## Step 6: Deploy Added/Updated Logical Units

1.  Deploy **Investigator** LU

    > After Deployment, Validate the following Cassandra tables are created
    under **k2system** keyspace:

1.  **get_details**

2.  **log_scan**

3.  **ivl\_\${luname}\_cons_detailed_stat**

<!-- -->

2.  Deploy **Web Services**

# How To Use

***Open Investigator in the Web Framework***

1.  In your Cloud Studio, Click menu at the top left of the screen
    (hamburger icon) and select **Investigator** to open the page.

    <img src="media/image5.png"
    style="width:2.91667in;height:3.00694in" />

2.  Notice three investigation categories

    1.  IID Search

    2.  Kafka Topics

    3.  IID Consumer

## ***IID Search page***

1. Enter the **LU Type** and **IID**

    <img src="media/image6.png" style="width:5.85208in;height:0.76875in" />

2.  Select desired categories.

3.  Click **Search**.

4.  Sub-tabs will appear in the search results.

    <img src="media/image7.png" style="width:3.17014in;height:0.59306in"/>

5.  Explore **System DB** tab

    1.  Click on System DB tab
    2.  Data from various table in the System DB will be displayed on the screen.

        <img src="media/image8.png" style="width:3.87847in;height:2.59236in" />

    3.  The data for the iidFinder cache k/d tables will not be
        displayed automatically due to its large size. To access this
        data, click the triangle icon to expand the cache tables.

        <img src="media/image9.png" style="width:4.12312in;height:2.02015in" />

6.  Explore **Lui Data** tab

    1.  Click on LUi Data tab
    2.  Data from various table in the LU will be displayed on the screen
        <img src="media/image10.png" style="width:4.25625in;height:2.59792in" />

7.  Explore **Delta Topics** tab

    1.  Click on Delta Topics tab
    2.  Messages for the specified instance in the Delta topic will be displayed
        <img src="media/image11.png" style="width:4in;height:2.57083i"/> 
    

8.  Explore **Log** tab

    1.  Click on Log tab

    2.  Select the desired time range, and click **SAVE**.
        
        <img src="media/image12.png" style="width:3.21944in;height:1.77083in" />
        
    3.  Log messages that are related to the GET execution of the specified
    instance will be displayed in a table format. You can download the
    provided log by clicking the following
    button:
        <img src="media/image13.png" style="width:5.82796in;height:1.43769in" />

<!-- -->

9.  If needed, minimize or remove tables by clicking the **"-"** or
    **"x"** buttons.

## ***Kafka Topics page***

1. In this page, navigate through the tabs using navigator table at the top of the page:

    <img src="media/image14.png" style="width:5.90972in;height:1.06875in" />

2. Explore **Messages** page

    1.  Navigate to **Messages** tab

    2.  Insert the mandatory inputs: **Search Type** and **Topic**

    3.  Insert optional inputs for enhanced search

    4.  Click **Search**
    
        <img src="media/image15.png" style="width:5.59028in;height:2.27431in" />

    5.  Hover over a specific message row to expand and view the full
        message data

3. Explore **Lag** page

    1.  Navigate to **Lag** tab

    2.  Insert the mandatory input: **Search Type**

    3.  Click **Search**

        <img src="media/image16.png" style="width:5.68611in;height:2.90625in"/>

## ***IID Consumer page***

1. In this page, navigate through the tabs using navigator table at the top of the page:
    
    <img src="media/image17.png" style="width:6.5in;height:1.18542in" />

2.  Explore **Summary** page

    1.  Navigate to **Summary** tab

    2.  Insert the mandatory inputs: **LU Type**

    3.  Edit the **Time-Window** input as need

    4.  Click the **Refresh** button

    5.  Summary data of each IID Consumer defined in the mtLUTopic is
        Displayed in the screen

    6.  Expand the data of a specific consumer by clicking on the "Show
        Details" button
        
        <img src="media/image18.png" style="width:4.84722in;height:2.22009in" />

3.  Explore **Current** Page

    1.  Navigate to **Current** tab

    2.  The currently running GET executions from the predefined IID
        Consumers are displayed on the screen

        <img src="media/image19.png" style="width:5.86111in;height:1.23611in" />

4.  Explore **History** Page

    1.  Navigate to **History** tab

    2.  Insert the mandatory inputs: **LU Type**, **Topic**, **Start
        Time**

    3.  Click **Seach**

    4.  History data of each GET execution executed by the predefined
        IID Consumers is displayed on the screen

    5.  To log SKIPPED messages, change the global:
        IVL_SKIPPED_IIDS_STATS
        
        <img src="media/image20.png" style="width:6.15486in;height:2.10972in" />

***Notes:***

1.  Table columns are adjustable (reorder, resize).

2.  Hover over long text rows to expand and view full content.
