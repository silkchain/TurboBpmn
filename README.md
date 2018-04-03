# TurboBPMN
BPMN execution engine on many blockchains. Now with support for Ethereum smart contract.

TurboBPMN is a Business Process Management System (BPMS) that runs on top of various blockchains and that relies on the translation of process models into smart contracts. More specifically, TurboBPMN accepts as input a process model specified in BPMN and generates a set of smart contracts that captures the underlying behavior. The smart contracts, written in Ethereum's Solidity language, can then be compiled and deployed to the public or any other private Ethereum network using standard tools. Moreover, TurboBPMN exhibits a REST API that can be used to interact with running instances of the deployed process models.

TurboBPMN also provides a set of modelling tools and an execution panel which interact with the underlying execution engine via the aforementioned REST API. The latter can also be used by third party software to interact in a programmatic way via TurboBPMN with the instances of business process running on the blockchain.

TurboBPMN code distribution in this repository contains two different folders.
The folder bpmn_core includes the implementation of the core components, execution_panel includes the code of a BPMN visualizer that serves to keep track of the execution state of process instances and to lets users check in process data, and services_manager contains the implementation for an external service used for demonstration purposes.

For running TurboBPMN locally, download the source code from the repository and follow the next steps to set up the applications and install the required dependencies.

## Installing testrpc

The first requirement is to install testrpc which is a Node.js based Ethereum client for testing and development. It uses ethereumjs to simulate full client behavior and make developing Ethereum applications. All the instructions about the installation can be found here: https://github.com/ethereumjs/testrpc.

> Please, be aware to start the testrpc server before running the applications TurboBPMN Core and Services Manager. In that respect, you only need to open a terminal on your computer and run the command:

     testrpc

## How to use TurboBPMN Core

Open a terminal in your computer and move into the folder __bpmn-core__. 

For installing the dependencies, run the comands 

     npm install
     gulp build

For running the application you use one of the following comands
 
     node ./out/www.js     
     
> If the process model has service tasks and consequently needs to interact with the services manager application, then you must run the services manager application and create the corresponding services before running TurboBPMN core.

By default the application will runs on http://localhost:3000.

The application provides a REST API to interact with the core of TurboBPMN. The following table summarizes the mapping of resource-related actions:

| Verb | URI                       | Description                                                            |
| -----| ------------------------- | ---------------------------------------------------------------------- |
| POST | /models                   | Registers a BPMN model (Triggers also code generation and compilation) |
| GET  | /models                   | Retrieves the list of registered BPMN models                           |
| GET  | /models/:mid              | Retrieves a BPMN model and its compilation artifacts                   |
| POST | /models/:mid              | Creates a new process instance from a given model                      |
| GET  | /processes/               | Retrieves the list of active process instances                         |
| GET  | /processes/:pid           | Retrieves the current state of a process instance                      |
| POST | /workitems/:wimid/:wiid   | Checks-in a work item (i.e. user task)                                 |
| POST | /workitems/:wimid/:evname | Forwards message event, delivered only if the event is enabled         |

From the bpmn_core folder is possible to run the script

     node demo_running_example_test.js
     
to register, create an instance and get the address of a sample process provided in the file __demo_running_example.bpmn__.


## How to use Execution Panel

Open a terminal in your computer and move into the folder __execution-panel__. 

For installing the dependencies, run the comand 

     npm install

For running the application use the comand 

     ng serve
     
Open a web browser and put the URL http://localhost:4200/.

You must use the button refresh to update the instances running, and then select one of the URLs obtained that will contain the address when it is running the smart contract. Then press the button __Open__. Here, you can see the enabled activities visualized in dark green. For executing any enabled activity, just click on it and fill the parameter info if required. All the execution of the process (including internal operations) can be traced from the terminals of __bpmn-core__.


 
