implementation of the BAdI. Because the BAdI uses plant number as the filter criterion, we're passing the filter value with the GET BADI statement using the FILTERS addition. Once we have the reference to the implementation, we can access its methods by using the CALL BADI statement.

As you can see, by implementing the BAdI we can avoid using the CASE statement from Listing 20.1 to handle plant-specific logic in the main program. Each plant can have its own implementation, which can be changed without changing the main program. If new plants are added, we can simply add new implementations to the BAdI.

Good object-oriented design calls for the separation of tasks. By implementing the BAdI, we separated the task of finding the plant and running the tasks specific to the plant. The program's job here is to find the plant, and the BAdI's job is to run plant-specific tasks. The program doesn't need to know what tasks are being performed for the plant, and the BAdI doesn't need to know how the program is determining the logic for each plant.

# 20.9 Enhancement Points

One major challenge with the enhancement concepts that we've discussed so far is that they're called at predefined locations in standard SAP programs and have fixed interfaces. They're sufficient to meet the requirements of customers most of the time, but they do have several limitations for customizing standard SAP applications. The whole concept behind these enhancements relies on SAP anticipating how customers might want to enhance standard SAP programs and correctly deciding where to provide the opening in the code.

The *Enhancement Framework* was introduced in SAP ERP 6.0. This framework brought the concept of enhancing SAP applications to a different level with the introduction of enhancement points.

*Enhancement points* allow you to bend standard SAP applications as you wish. Enhancement points are source code plugins added to the source code of the standard SAP programs directly. These source code plugins are compiled with the main program and are as good as writing the code directly in the main program.

There are two types of enhancements available: explicit and implicit. In the following subsections, we'll discuss each type.