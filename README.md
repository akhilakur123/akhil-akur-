# akhil-akur-

                                i--;

                                printf("\b");

                                printf(" ");

                                printf("\b");

                                pass[i]=getch();

                            }

                            else

                            {

                                printf("*");

                                i++;

                                pass[i]=getch();

                            }

                        }

                        pass[i]='\0';

                        i=0;

                        printf("\n\tCONFIRM PASSWORD:");

                        confirm[0]=getch();

                        while(confirm[i]!='\r')

                        {

                            if(confirm[i]=='\b')

                            {

                                i--;

                                printf("\b");

                                printf(" ");

                                printf("\b");

                                confirm[i]=getch();

                            }

                            else

                            {

                                printf("*");

                                i++;

                                confirm[i]=getch();

                            }

                        }

                        confirm[i]='\0';

                        if(strcmp(pass,confirm)==0)

                        {

                            fp=fopen("SE","wb");

                            if(fp==NULL)

                            {

                                printf("\n\t\tSYSTEM ERROR");

                                getch();

                                return ;

                            }

                            i=0;

                            while(pass[i]!='\0')

                            {

                                ch=pass[i];

                                putc(ch+5,fp);

                                i++;

                            }

                            putc(EOF,fp);

                            fclose(fp);

                        }

                        else

                        {

                            printf("\n\tTHE NEW PASSWORD DOES NOT MATCH.");

                            choice=1;


                        }


                    }

}while(choice==1);


    printf("\n\n\tPASSWORD CHANGED...\n\n\tPRESS ANY KEY TO GO BACK...");

    getch();

}


void deleterecord( )

{

                system("cls");

                FILE *fp,*fptr ;

                struct record file ;

                char filename[15],another = 'Y' ,time[10];;

                int choice,check;

                printf("\n\n\t\t*************************\n");

                printf("\t\t* WELCOME TO DELETE MENU*");

                printf("\n\t\t*************************\n\n");

                check = password();

                    if(check==1)

                    {

                        return ;

                    }


                while ( another == 'Y' )

                {

                printf("\n\n\tHOW WOULD YOU LIKE TO DELETE.");

                printf("\n\n\t#DELETE WHOLE RECORD\t\t\t[1]");

                printf("\n\t#DELETE A PARTICULAR RECORD BY TIME\t[2]");


                do

                {

                        printf("\n\t\tENTER YOU CHOICE:");

                        scanf("%d",&choice);


                    switch(choice)

                        {

                            case 1:

                            printf("\n\tENTER THE DATE OF RECORD TO BE DELETED:[yyyy-mm-dd]:");

                            fflush(stdin);

                            gets(filename);

                            fp = fopen (filename, "wb" ) ;

                            if ( fp == NULL )

                            {

                                printf("\nTHE FILE DOES NOT EXISTS");

                                printf("\nPRESS ANY KEY TO GO BACK.");

                                getch();

                                return ;

                            }

                            fclose(fp);

                            remove(filename);

                            printf("\nDELETED SUCCESFULLY...");

                            break;


                            case 2:

                            printf("\n\tENTER THE DATE OF RECORD:[yyyy-mm-dd]:");

                            fflush(stdin);

                            gets(filename);

                            fp = fopen (filename, "rb" ) ;

                            if ( fp == NULL )

                            {

                                printf("\nTHE FILE DOES NOT EXISTS");

                                printf("\nPRESS ANY KEY TO GO BACK.");

                                getch();

                                return ;

                            }

                            fptr=fopen("temp","wb");

                            if(fptr==NULL)

                            {

                                printf("\nSYSTEM ERROR");

                                printf("\nPRESS ANY KEY TO GO BACK");

                                getch();

                                return ;

                            }

                            printf("\n\tENTER THE TIME OF RECORD TO BE DELETED:[hh:mm]:");

                            fflush(stdin);

                            gets(time);

                            while(fread(&file,sizeof(file),1,fp)==1)

                            {

                                if(strcmp(file.time,time)!=0)

                                fwrite(&file,sizeof(file),1,fptr);

                            }


                            fclose(fp);

                            fclose(fptr);

                            remove(filename);

                            rename("temp",filename);

                            printf("\nDELETED SUCCESFULLY...");

                            break;


                    default:

                            printf("\n\tYOU ENTERED WRONG CHOICE");

                            break;

                    }

                }while(choice<1||choice>2);



                    printf("\n\tDO YOU LIKE TO DELETE ANOTHER RECORD.(Y/N):");

                    fflush(stdin);

                    scanf("%c",&another);

                }

                printf("\n\n\tPRESS ANY KEY TO EXIT...");

                getch();

}
