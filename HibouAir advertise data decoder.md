# HibouAir advertised data decode
## Python
The following function decodes the advertised data into json format. 
example of advertised data 0201061AFF5B0705030581CA7D084127D300AE01FE05000009002100000000


    def  adv_data_decode(data):
	    pos  =  data.find("5B070")
	    temp_hex  =  convertNumber(data, 22, 4)
	    if  temp_hex  >  1000:
		    temp_hex  = (temp_hex  - (65535  +  1)) /  10
	    else:
		    temp_hex  =  temp_hex  /  10

	    env_data  = {
		    "boardID": data[pos  +  8 : pos  +  8  +  6],
		    "type": int(data[pos  +  6 : pos  +  6  +  2], 16),
		    "light": convertNumber(data, 14, 4),
		    "pressure": convertNumber(data, 18, 4) /  10,
		    "temperature": temp_hex,
		    "humidity": convertNumber(data, 26, 4) /  10,
		    "voc": convertNumber(data, 30, 4),
		    "co2": int(data[pos  +  46 : pos  +  46  +  4], 16),
	    }
	    return  env_data

  



## JavaScript
The following function decodes the advertised data into json format. 
example of advertised data 0201061AFF5B0705030581CA7D084127EBFFAE01FE05000009002100000000

    const  advDataDecode  = (data, id) => {
    let  pos  =  data.indexOf('5B070');
    let  tempHex  =  parseInt('0x'  +data.substr(pos  +  22, 4).match(/../g).reverse().join(''));
    if (tempHex  >  1000) tempHex  = (tempHex  - (65535  +  1)) /  10;
    else  tempHex  =  tempHex  /  10;
    return (envData  = {
	    boardID:  data.substr(pos  +  8, 6),
	    type:  parseInt(data.substr(pos  +  6, 2)),
	    light:  parseInt('0x'  +data.substr(pos  +  14, 4).match(/../g).reverse().join('')),
	    pressure:parseInt('0x'  +data.substr(pos  +  18, 4).match(/../g).reverse().join('')) /  10,
	    temp:  tempHex,
	    hum:parseInt('0x'  +data.substr(pos  +  26, 4).match(/../g).reverse().join('')) /  10,
	    voc:  parseInt('0x'  +data.substr(pos  +  30, 4).match(/../g).reverse().join('')),
	    pm1:parseInt('0x'  +data.substr(pos  +  34, 4).match(/../g).reverse().join('')) /  10,
	    pm25:parseInt('0x'  +data.substr(pos  +  38, 4).match(/../g).reverse().join('')) /  10,
	    pm10:parseInt('0x'  +data.substr(pos  +  42, 4).match(/../g).reverse().join('')) /  10,
	    co2:  parseInt('0x'  +  data.substr(pos  +  46, 4)),
	    vocType:  parseInt('0x'  +  data.substr(pos  +  50, 2)),
	    });
    };


## Example output

    {  
	    boardID:  "0581CA",  
	    co2:  0,  
	    hum:  43,  
	    light:  2173,  
	    pm1:  0,  
	    pm10:  3.3,  
	    pm25:  0.9,  
	    pressure:  1004.9,  
	    temp:  21.1,  
	    ts:  "2024/03/11 14:50:59",  
	    type:  3,  
	    voc:  1534,  
	    vocType:  0  
    }

