```
```c
} st_rec;
Void main()
{
    int ch;
    St_rec rec;
    FILE *fp;
    Fp= fopen("employee.rec","wb");
    Printf("\n enter the empno");
    Printf("type ctrl+z to stop\n");
    /*read from keyboard and write to file*/
    While(scanf("%u%c%d",&rec.empno,&rec.name,&rec.salary) !EOF)
    Fwrite(&rec,sizeof(rec),1,fp);
    Fclose(fp);
    Printf("\n");
    /* read from file and write on screen*/
    Fp=fopen("employee.rec","rb");
    /* while loop terminates when fread returns 0*/
    While ( fread(&rec,sizeof(rec),1,fp))
    Printf("%5u%-10c$3d\n",rec.empno,rec.name,rec.salary);
    int addrecord ();
    int removerecord();
    int searchrecord ();
    Switch(ch)
    {
    Case 'a': int addrecord()
        {
        While(scanf("%u%c%d",&rec.empno,&rec.name,&rec.salary) !EOF)
        fwrite(&rec,sizeof(rec),1,fp);
        fclose(fp);
        }
        break;
    Case 'd': int removerecord(const char*employeerecord.index);
    Break;
    Case 's' : int searchrecord()
        {
        Fp=open("employee.rec","rb");
        /* while loop terminates when fread returns 0*/
        While ( fread(&rec,sizeof(rec),1,fp))
        Printf("%5u%-10c$3d\n",rec.empno,rec.
        name,rec.salary);
        }
        fclose(fp);
    }
    fclose(fp);
}
```
```