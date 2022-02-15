<div align="center">

<span style="color:#F74165">

# CPE | CVSS similar format for nodes set exchanges
## THREAD <span style="color:#28E9C3">=></span> KLYNTAR
</span>

</div>

</br></br>

<span style="color:#28E9C3">

# <b>Authors & Metadata</b>

</span>

<b>Date</b>:05.02.2022</br>
<b>Author</b>:Vlad Chernenko</br>
<b>Contacts</b>:[Telegram:@VladChernenk0](https://t.me/Vlad_Chernenk0)//(last is zero,not letter "o")

</br></br>

<span style="color:#28E9C3">

# <b>Motivation</b>

</span>

</br>

To make the process of initial connection(and further connections) between different nodes on <b>KLYNTAR</b> more advanced I propose to add some more logic to default API routes(stored in <i>KLY_Routes/api.js</i>) and configuration without code changes. As default nodes use <b>Phisher_Yeits algorithm</b> to response other nodes with random subsets of nodes. In the same time, you also can set static nodes sets in your configuration of symbiote you're working on. But it will be better to get sets of nodes following some advanced logic.

</br>

### For example,when your node instance tries to get the set of nodes,it sends <b>REGION</b> with the query

```js

fetch(CONFIG.SYMBIOTES[symbioteID].CONTROLLER.ADDR+'/nodes/'+symbioteID+'/'+CONFIG.SYMBIOTES[symbioteID].REGION)

    .then(r=>r.json())
    
    .then(
                
        nodesArr=>{

            //...further logic

        }
    
    )

```

</br>

<b>Response node holds some following values to go through Phisher_Yeits algorithm and send you response</b>

```js

 "NODES":{

                "EU":[
                    "https://0.mynearpub.com:7777",
                    "https://1.mynearpub.com:7777",
                    "https://2.mynearpub.com:7777",
                    "https://3.mynearpub.com:7777",
                    ...
                ],

                "NA":[
                    "https://0.mynearpub.com:7777",
                    "https://1.mynearpub.com:7777",
                    "https://2.mynearpub.com:7777",
                    "https://3.mynearpub.com:7777",
                    ...
                ],

                ...


```
</br></br>

<span style="color:#28E9C3">

# <b>Proposition</b>

</span>

## The basic proposition is to make <b>REGION</b> not only location close to the node,let's allow different subsets of nodes to have own rules</br></br>

<b>With such flexible format it may looks like this</b>

```js

 "NODES":{

                "EU_FR:MULTI*I*C@20":[
                    "https://0.mynearpub.com:7777",
                    "https://1.mynearpub.com:7777",
                    "https://2.mynearpub.com:7777",
                    "https://3.mynearpub.com:7777",
                    "https://4.mynearpub.com:7777",
                    "https://5.mynearpub.com:7777",
                    ...
                ],
                "AS_CN_BEIJING":[
                    "https://0.mynearpub.com:7777",
                    "https://1.mynearpub.com:7777",
                    "https://2.mynearpub.com:7777",
                    "https://3.mynearpub.com:7777",
                    "https://4.mynearpub.com:7777",
                    "https://5.mynearpub.com:7777",
                    ...
                ],

                ...

```

Such format allows different symbiotes or subset of nodes to use own rules. For example, if you're living in Beijing, and your node configuration is</br>

```js
"REGION":"AS_CN"
```

It will be better to change to

```js
"REGION":"AS_CN_BEIJING"
```

The first example,however,has even more advaced format. <b>KLYNTAR</b> definitely supports different type of data sharing(e.g sets of blocks,accounts state,conveyors metadata and so on). Instead of set

```js
"REGION":"EU_FR"
```

You can set

```js
"REGION":"EU_FR:MULTI*I*C@20"
```

And it means that received subset supports <b>MULTI-multitransfer</b>(transfer many blocks at one time), <b>I-transfer InstantBlocks of symbiote</b>, <b>C-transfer ControllerBlocks of symbiote</b>.Additional value 20 after the @ may be interpreted like <b>"all nodes of this group accepts not more than 20 incoming connections"</b>,so for example,don't share them(not to lose your treasure like this fast and multifunctional nodes😅).

</br></br>

<span style="color:#28E9C3">

# <b>How it can be implemented</b>

</span>

As I've promised you,it can be implemented without great code changes. The first step-if it was announced that some source support such advaced mechanisms,change your <b>REGION</b> following instructions.
On the other side,insofar as <b>KLYNTAR</b> supports raw control and access to root workflow of process via custom runtime scripts in <b>KLY_Custom/<YOUR_PROJECT_DIR>/<SCRIPT_ITSELF></b>,you can get access to your sets of nodes for each chain, handle newbies from your local list and,using value of <b>REGION</b>,provide your own operations over sets.</br></br>

<b>For example,let's take a look how it's possible</b>

```js

//___________________KLY_Custom/MY_NODES_TRACKER_VENOM/track.js___________________

//import mapping of supported symbiotes
import {symbiotes} from '../../klyn74r.js'

//Get an array of nodes for 
let nodes=symbiotes.get(<SYMBIOTE_ID>).NEAR,

    rule=CONFIG.SYMBIOTES[<SYMBIOTE_ID>].REGION//get for example EU_FR:MULTI*I*C@20


//...provide following logic here

```