
## 9.2.3 Retrieving values from the ACD file

To retrieve C pointers to these data items the following code is used:

```
seqout = ajAcdGetSeqoutall("outseq");
seqall = ajAcdGetSeqall("sequence");
```

Similarly, to retrieve the value of the simple data type variable firstonly:

```
firstonly = ajAcdGetBoolean("firstonly");
```

You can see that the argument to the ajAcdGet* functions is the name of the ACD definition which is to be retrieved.

## 9.2.4 Sequence handling

To iterate through the input sequences and load a sequence into memory the following code is used:

```
while(ajSeqallNext(seqall, &seq))
{
    ajSeqoutWriteSeq(seqout, seq);
    if(firstonly)
        break;
}
```

ajSeqallNext is called in a loop to retrieve consecutive sequences in turn from the input stream. The second argument (&seq) sets the pointer to the current sequence in the stream. ajSeqoutWriteSeq is used to write this sequence to the output stream seqout. The loop will terminate after the first sequence if firstonly has been set.

## 9.2.5 Exiting cleanly

The output stream is closed by calling ajSeqoutClose(). The application terminates cleanly with the call embExit() before returning 0 to the operating system:

```
ajSeqoutClose(seqout);
embExit();
return 0;
}
```

## 9.3 Inbuilt functionality

seqret has rich inbuilt functionality:

- It can read and write any sequence format that EMBOSS supports (see the EMBOSS User's Guide), which includes all the common formats.
- It uses the powerful USA syntax (see the EMBOSS User's Guide) for specifying the location and format of the sequence data.
- seqret can read one or more sequences from a database, file, listfile (file of USAs), the command line or the output of other programs and can then write them to a file, database or to stdout which can be redirected to another program. It's therefore useful for extracting sequences from databases and displaying them.
- seqret supports many command line options which are not listed in the ACD file. These include global and datatype-specific qualifiers. Many others are available and may be used in combination, providing greater flexibility without the requirement for any additional programming.
- It supports global qualifiers (see the EMBOSS User's Guide) which are available to all EMBOSS applications.
- It supports various datatype-specific qualifiers (see the EMBOSS User's Guide); in this case, the sequence datatypes which include the seqall : sequence input and seqoutall : outseq output definitions from the ACD file.

For example, you can specify the input and output formats by using the -sformat FormatName (input) and -osformat FormatName (output) options. If you don't specify the input format it will try all known formats until one succeeds, and if you don't specify the output format then FASTA will be used by default. seqret is useful for reformatting sequences, perhaps in preparation for input to another program.

The -sbegin and -send options specify the start and end position of a subsequence in the input sequence. This fragment is written to the output file, therefore seqret is useful for simple extraction of sequence regions. The -sreverse switch will use the reverse complement of a nucleic acid sequence.

As you've seen from seqret.c, no application code is needed to benefit from this inbuilt functionality. What's more, as new sequence formats are added to EMBOSS, seqret will automatically be able to use them; no application code needs to change. It should be obvious then that this inbuilt functionality saves you, as a software developer, a great deal of time.

## 9.3.1 Example usage

Examples illustrating a few of the many use cases of seqret are shown below.

Here seqret is being used to retrieve the entry 5HT1D_FUGRU from the SwissProt database and write the entry out in FASTA format:

```
% seqret
Reads and writes (returns) sequences
Input (gapped) sequence(s) : swissprot:5HT1D_FUGRU
Output sequence [5ht1d_fugru.fasta] :
% more 5ht1d_fugru.fasta
>5HT1D_FUGRU P79748 5-hydroxytryptamine receptor 1D (5-HT-1D)
MELDNNSLDYFSSNFTDIPSNTTVAHWTEATLLGLQISVSVVLAIVTLATMLSNAFVIAT
IFLTRKLHTPANFLIGSLAVTDMLVSILVMPISIVYTVSKTWSLGQIVCDIWLS SDITFC
TASILHLCVIALDRYWAITDALEYSKRRTMRRAAVMVAVVWVISISISMPPLFWRQAKAH
EELKECMVNTDQISYTLYSTFGA FYVPTVLLIILYGRIYVAARSRIFKTPYSYGKRFTTA
QLIQTSAGSSLCSLNSASNQEAHLHSGAGGEGGGS PLFVNSVKVKLADNVLERKR LCAAR
```

The same thing could be achieved by using the USA (see the EMBOSS User's Guide) mechanism to specify the same input and output sequences on the command line:

```
seqret swissprot:5HT1D_FUGRU fasta:5ht1d_fugru.fasta
```

This example retrieves all of the sequences from the input stream. Not a very sensible thing to do, but it illustrates that the USA mechanism supports wildcard specification of sequences:

```
% seqret swissprot:"*"
Reads and writes (returns) sequences
Output sequence [ubr5_rat.fasta]: all.fasta
% more all.fasta
>UBR5_RAT Q62671 E3 ubiquitin-protein ligase UBR5 (6.3.2.-)
MMSARGDFLNYALSLMRSHNDEHSDVLPVLDVCSLKHVAYVFQALIYWIKAMNQQTTLDT
PQLERKRTRELLELGIDNEDSEHENDDDTSQSATLNDKDDESLPAETGQNHPFFRRSD SM
TFLGCIPPNPFEVPLAEAIPLADQPHLLQPNARKEDLFGRPSQGLYSSSAGSGKCLVEVT
MDRNCLEVLPTEKMSYAANLKNVMNMQNRQKKAGEDQSMLAEEADSSKPGPSAHDVAAQLK
SSLLLAEIGLTESEGPLTSFRPQCSFMGMVISHMLLGRWRLSLELFGRVFMEDVGAEPG
SILTELGGFEVKESKFREMEKLRNQQSRDLSLEVDRDRDLLIQQTMRQILNNHFGRRCAT
TPMAVHRVKVTFKDEPEGESGVARSFYTAIAQAFLSNEKLPLNLDCIQNANKGTHTSLMQR
LRNRGERDREREREREMRRSGLRAGSRRDRDRDFRRQLSIDTRPFPASEGNPSDDP DP
LPAHRQALGERLYPRVQAMQPAFASKITGMLELSPAQLLLLLLASEDSLRARVEEAMELI
VAHGRENGADSILDLGLLDSSEKVQENRKHGGSSRSVVDMDLDDTDGDDDNAPLFYQPGK
RGFYTPRPGKNTEARLNCFRNIGRILGLC LLQNELCPITLNRHVIKVLLGRKVNWHDFAF
FDPVMYESLRQLILASQSSDADAVFSAMDLAFAVDLCKEEGGGQVELIPNGVNI PVTPQN
VYEYVRKYAEHRMLVVAEQPLHAMRKGLLDVLPKNSLEDLTAEDFR LLVNGCGEVNVQML
ISFTSFNDESGENAEKLLQFKRWFSIVERMSMTERQDLVYFWTSSPSLPASEEGFQPMP
SITIRPPDDQHLPTANT CISRLYVPLYSSKQILKQLLLLAIKTKNFGFV
>5HT1D_FUGRU P79748 5-hydroxytryptamine receptor 1D (5-HT-1D) (5HT1D)
MELDNNSLDYFSSNFTDIPSNTTVAHWTEATLLGIQISVSVVLAIVTLATMLSNAFVIAT
IFLTRKLHTPANFLIGSLAVTDM LVSILVMPISIVYTVSKTWSLGQIVCDIWLSSDITFC
TASILHLCVIALDRYWAITDALEYSKRRTMRRAAVMVAVVWVISISISMPP LFWQAKAH
EELKECMVNTDQISYTLYSTFGAFYVPTVLLIILYGRIYVAARSRIFKTPSYSGKRFTTA
QLIQTSAGSLSLSLNSASNQEAHLHSGAGGEGGGSPLFVNSVKVKLADNVLERKRLCAAR
ERKATKTLGIILGAFIICWLPFFVVTLVWAICKECSFDPLLFDVFTWLGYLNSLINPVIY
TVF NDEFKQAFQKLIKFRR
>ACTB1_FUGRU P68142 Actin, cytoplasmic 1 (Beta-actin A)
MEDEIAALVVDNGSGMCKAGFAGDDAPRAVFPSIVGRPRHQGVMVGMGQKDSYVGDEAQS
KRGI LT LKYPIEHGIVTNWDDMEKIWHHTFYNELRVAPEEHPVLLTEAPLNPKANREKMT
QIMFETFNTAMYVAIQAVLSLYASGRTTGI VMDSGGDVTH TVPIYEGYALPHAILRLDL
... data omitted
```

The following example illustrates the use of the -firstonly option. This is an advanced option therefore will never be prompted for; whenever used it has to be specified on the command line:

```
% seqret swissprot:"" -outseq all.fasta -firstonly
Reads and writes (returns) sequences
% more all.fasta
>UBR5_RAT Q62671 E3 ubiquitin-protein ligase UBR5 (6.3.2.-)
MMSARGDFLNYALSLMRSHNDEHSDVLPVLDVCSLKHVAYVFQALIYWIKAMNQQTTLDT
PQLERKRTRELLELGIDNEDSEHENDDDTSQSATLNDKDDESLPAETGQNHPFFRRSD SM
TFLGCIPPNPFEVPLAEAIPLADQPHLLQPNARKEDLFGRPSQGLYSSSAGSGKCLVEVT
MDRNCLEVLPTKMSYAANLKNVMNMQNRQKKAGEDQSMLAEEADSSKPGPSAHVDVAAQLK
SSILAAEIGLTESKGPLLTSFRPQCSFMGMVTSHDMLLGRWRLSLELFGRVFMEDVGAEPG
SILTEIGGFEVEKSKEFREMEKLRNQQSRDL SLEVDRDRDLLIQQTMRQLNNHFGRRCAT
TPMAVHRVKVTFKDEPEGSGSVARSFYTAIAQAFLSNEKLPNLDCIQNANKGTHTSLMQR
LRNRGERDREREREREMRRSSGLRAGSRRDDRDFRQRLSIDTRPFRPASEGNPSDDPDP
LPAHRQALGERLYPRVQAMQPAFASKITGMLELSLPAQLLLLLLASEDSLRARVEEAMELI
VAHGRENGADSILDLGLLDSSEKVQENRKRHGSSRSVVDMDLDDTDDGDDNAPLFYQPGK
RGFYTPRPGKNTEARLNCFRNIGRILGLCLLQNELCPITLNRHVIKVLLGRKVNVWHDFAF
FDPVMYESLRQLILASQSSDADAVFSAMDLAFAVDLCKEEGGGQVELIPNGVNIPVTPQN
VYEYVRKYAEHRMLVVAEQPLHAMRKGLLDVLPKNSLEDLTAEDFRLLVNCGEVNVQML
ISFTSFNDDESGENAEKLLQFKRWFWSIVERMSMTERQDLVYFWTS SPSLPASEEGFQMP
```

Here, usage information is being generated by using the -help global qualifier:

```
% seqret -help
Standard (Mandatory) qualifiers:
[-sequence] seqall (Gapped) sequence(s) filename and optional
format, or reference (input USA)
[-outseq] seqoutall Sequence set(s) filename and optional format
(output USA)
Additional (Optional) qualifiers: (none)
Advanced (Unprompted) qualifiers:
-feature boolean Use feature information
-firstonly boolean Read one sequence and stop
General qualifiers:
-help boolean Report command line options. More
information on associated and general
qualifiers can be found with -help -verbose
```

In the example below, the sequence-specific command line options -sbegin and -send are used to specify a sequence region:

```
% seqret swissprot:5HT1D_FUGRU -sbegin 10 -send 20 fasta:5ht1d_fugru.fasta
Reads and writes (returns) sequences
% more 5ht1d_fugru.fasta
>5HT1D_FUGRU P79748 5-HYDROXYTRYPTAMINE 1D RECEPTOR (5-HT-1D) (SEROTONIN RECEPTOR).
YFSSNFTDIPS
```

## 9.4 Documentation (seqret.html)

The end-user documentation is organised into sections for easy navigation. You can see this for yourself in the online application documentation:

http://emboss.open-bio.org/rel/dev/apps/seqret.html

For more information see Chapter 8, application documentation standards.
