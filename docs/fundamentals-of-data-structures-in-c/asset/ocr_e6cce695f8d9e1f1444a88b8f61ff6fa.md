```
```c
switch(ch)
{
    case 0 :
        display_menu();
        break;

    case 1 :
        createGraph();
        break;

    case 2 :
        insertVertex();
        break;

    case 3 :
        printf("\n Enter the Starting & Ending Vertex to
            insert Edge : ");
        scanf("%d %d, &vs, &ve);
        insertEdge(vs, ve);
        break;

    case 4 :
        printf("\n Enter the Vertex to delete : ");
        scanf("%d", &vd);
        deleteVertex(vd);
        break;

    case 5 :
        printf("\n Enter the Starting & Ending Vertex to
            delete Edge : ");
        scanf("%d %d, &vs, &ve);
        deleteEdge(vs, ve);
        break;

    case 6 :
        viewGraph();
        break;

    default :
        printf("End of run of your program . . .");
        exit(0);
}
}
```
```