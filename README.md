# c--pack-like-php
C++ pack like php
```c++
#pragma pack(1)
struct bindData
{
	unsigned int len;
	unsigned int command;
	unsigned int status;
	unsigned int snd_fb;
	unsigned int rcv_fb;
	char account[11];
	char pass[9]; 
	char sys_type[13]; 
	unsigned int version; 
};
#pragma pack(0)


using boost::asio::ip::tcp;

template <typename T>
std::string pack( const T& data ) {
	char toStr[sizeof(data)];
	memcpy(toStr, &data, sizeof data);

 	std::string buffer;
 	for( int i = 0; i < sizeof(toStr); i++ ) {
 		buffer += toStr[i];
 	}

 	return buffer;
}
```

# Usage : 

```c++
	bindData data;
	data.len = 57; 
	data.command = 0x65;
	data.status = 0;
	data.snd_fb = 0xffffffff;
	data.rcv_fb = 0xffffffff;
	memcpy( &data.account, "...\0", 6 );
	memcpy( &data.pass, "...\0", 8 );
	memcpy( &data.sys_type, "", 0 );
	data.version = 0x10;

	std::string buffer = pack<bindData>( data );
	int msize = sizeof( data );
	std::cout <<  msize << std::endl;
	std::cout <<  buffer << std::endl;
```
