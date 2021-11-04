# Generative art minting on AllEditions.art

**PLEASE NOTE The All Editions minting platform is a work in progress**  

All Editions streamlines the minting of new generative art and the creation of an associated NFT on the OpenSea marketplace.

The generative engine uses a paper.js script which is run at the time of mint to create a new and unique output tied to a token ID. Your script should use the supplied token variable to set any seed values for random generators so the output is consistent each time it’s run for that mint.

Once a piece is minted the system will output a source SVG and PNG thumbnail that is used to represent the minted artwork. 

In order to use All Editions to mint your generative NFT's you'll need the following things
- A MetaMask wallet
- An OpenSea account
- A working knowledge of javascript

# Get Started

1. Sign in to https://alleditions.art
1. Join the Discord: https://discord.gg/Ywy9u9tfUK

# Project Settings

### Title
The title that will be shown publicly to end users. Hit the refresh button after changing a name if you want to update the URL. on Limit

### Edition Limit
How many total editions will be minted before it's closed. Note this does not count or include the 00 genesis mint. 

### Mints per wallet
The max number of editions that a wallet is allowed to mint. This is a great way to restrict how many peices a single individual can mint. 

### Minting price
The amount a user will need to pay in Ether to mint an edition. Leave blank or set as 0 if you want people to be able to mint for free using only a signed request. Please read about gas fees in the minting process when setting prices. 

### Minting wallet
The Ether wallet that minting fees will be deposited into. It's recommended that this 

### OpenSea Collection
The unique id of the OpenSea collection you plan on minting the NFT too. You can find this at the end of the collciton URL. 

### About
A short bit about the project and why it's compelling. 

### Additional info
Any additional information you want to share. This is formatable text so it can inlclude links, etc.  

### Early Minting Reservations
Enable early Minting to let a certain number of people sign up to get early minting access, which will open as soon as the number of people you set has been reached. Early minting will be restricted to only the wallets of those who signed up for the number of minutes you choose. 

## Ownership Perks
***Please note at this time verified ownership works on Ethereum mints only, Polygon mints only reflecting the minting owner until OpenSea releases their V2 api and exposes Polygon ownership data.***

### Printable
Allow verified owners to purchase a physical version of the artwork. 

### Community
Provide verified owners a link to join an exclusive community. Perfect for discord or slack. 

### Special Features
Anything else you want to allow only verified owners to see. 

## Additional Settings

### Waitlist
Let people sigh up to be notified when it goes live. This is shown only when the project isn't live and automatically sends an email to people on the waitlist as soon as the project is set live. 

### Public galleries
Allow you project to be shown in public galleries (this is a future feature)

### Artists
Select the teammates that should be shown as the artist on the minting screen. 

### Teammates
Add more people to help manage the projet and minting of peices. 

# Scripting

All Editions supports the following built in script functions. 

### paper.js
This is the core library upon which the generative engine is built. Your script should always be contained inside a paperscript block.    
```
<script type="text/paperscript" canvas="myCanvas">    
  // Generative script goes here
</script>
```

### Token variable
At minting a random value is created and passed through using the token variable. You should use the token variable to set any seed values for random generators so the generated output is always the same for a given token. 
`var seed = token;`

### Traits variable 
After an edition is minted it passes back the traits variable which is stored and displayed in the minting screen. 
`traits = "800x800";`

Additional characteristic variables are planned for the future, Please inquire if you need something specific. 

### 3D Perlin Noise 
The Perlin noise generator is a great way to generate random values that are more natural and organic for x, y, and z dimensions of an artwork. 
```
var noise = new perlinNoise3d();
noise.noiseSeed(seed);
```

### chance.js 
 An additional random function set is provided through the chance.js library. 
`var chance1 = new Chance(seed);`

## The script editor

### Saving
When you are satisfied with the edits you have made on a script you can save it. Any changes made will be lost if you navigate away from the page without saving. 
Once a project is LIVE the script can no longer be edited. If you need to fix an issue after it's live. You can pause the minting by taking it out of LIVE mode and editing the script. 

### Animations
Most of the time scripts are about generating a static SVG file. However you may choose to add animations. If you do check this box and the full script will run every time the generated output is loaded instead of the SVG. 

### Random token generation
When testing out your script it's recommended that you test the output with a multitude of different random tokens to insure consistency in output. Hit the refresh button to generate a new token or paste in a specific one if you want to see the output for a specific value. 

### SVG output
If your project relies on the SVG file for additional functionality such as printing of the image. You can turn on SVG outputs for the generator and confirm the actual SVG file is formatted how you want it. 

### Contained Script
In addition to the image each time the script is generated it will also output the full self contained HTML version of the script. 
Offline editing -  Becuase of the way the generator works errors are not displayed in console so it's often helpful to take this output and edit it locally using console to troubleshoot errors until you have the output you desire. Then copy and paste back in just the `<script type="text/paperscript" canvas="myCanvas">` element into the script editor.
    
# Going live
All Editions helps streamline the process of minting generative art and getting it onto the blockchain using OpenSea's lazy minting process. But it's important to realize it's not 100% automatic and has a bit of manual intervention required. 

1. User connects MetaMask to All Editions
1. User mints an edition either by paying the ETH price or signing a free transaction
1. All Editions waits for 6 transaction confirmations from etherscan if it's a priced mint. 
1. The edition number is fixed and the script runs client side to generate the SVG
1. The SVG is stored along with a PNG file that is used fro thumbnails. 
1. The artists receives a notification and manually mints the NFT on OpenSea using the minting data provided (takes approximately 15-20 Seconds)
1. The artist transfers the NFT to the minter and marks the mint as complete.
  
## Choosing a Blockchain to mint on
When minting the NFT it will go into a collection the artist creates on OpenSea. There are two options for what chain the collection is on and each of them have tradeoff that you will want to consider. 

### Ethereum (ETH)
The most active blockchain on OpenSea with the most users able to buy and sell on becuase they have Ether. This blockchain currently has incredibly high gas fees so for example transferring an NFT after it's minted could cost upwards of 0.01 Ether. So it's better suited for high priced mints as a good portion of the Ether collected at mint could go towards transfering the NFT to the minters wallet.   

### Polygon (MATIC)
Polygon is a sidechain that address the high "gas" fees of Ether and facilitates virtually free transactions. In fact transfering an NFT is currently free so it is great for a larger mint where the price is low or for giveaways. 

## Minting Scenarios

### Sign & Transfer
The user initiates the mint using a MetaMask wallet and signs the transaction. This costs the user nothing to mint. The artist then creates the NFT on OpenSea and transfers it to the wallet the user minted with. 

### Buy & Transfer
The user initiates the mint using a MetaMask wallet and transfers the minting price in eth to the minting wallet associated with the series. The artist then creates the NFT on OpenSea and transfers it to the wallet the user minted with. It’s recommended the minting price be at least 0.015eth to fully cover gas fees of transferring if the NFT is going to be created on the Ethereum Mainnet.

### Sign & Buy
The user initiates the mint using a MetaMask wallet and signs the transaction agreeing to complete the purchase on OpenSea within 3 days. The artist then creates the NFT on OpenSea and sets it for sale only to the holder of the minting wallet.
Reserve & Buy - The user initiates the mint using a MetaMask wallet and transfers a percentage of the full minting price in eth to the minting wallet associated with the series. The artist then creates the NFT on OpenSea and sets it for sale only to the holder of the minting wallet.

## Minting the Genesis edition
Before you go live it's recommended that you mint the Genesis edition to confirm everything is working correctly and to establish an image for the series. After minting the genesis edition you have a


# Minting each NFT
Once a person has succesfully minted an edition all teammates are emailed a notification letting them know that the NFT needs to be minted on OpenSea. 

To mint the NFT go into the minting section of the project and select the NFT's needed tab and follow these steps. 

1. Confirm the image has been generated, if not click on the edition title to go to the NFT and let it render client side. 
2. Click the download PNG button to get the preview image. 
3. Click the copy title button to copy the title to the clipboard
4. Click the OpenSea button to open a new creation window 
5. Drop the PNG image into the image area
6. Paste the title into the Name field
7. Click the copy URl button and paste it into the External link field
8. Click the copy description button and paste it into the description field
9. Add any traits are other aspects you want to the OpenSea form
10. Click the create button and wait for the NFT to be created
11. Copy the OpenSea URl and paste it into the OpenSea URL field in the minting list
12. Copy the minting wallet
13. Click the transfer buton on the NFT and enter in the minting wallet
14. Once the transfer has been confirmed click the done or notify button 
15. Repeat as need until all NFTs have been created. 


