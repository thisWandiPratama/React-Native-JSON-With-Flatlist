# React-Native-JSON-With-Flatlist
Membuat Data JSON dan Mengimplementasikan Di React Native Dengan Component FlatList Kemudian Menglemparkan Data menggunakan State Params React Navigation.

## Data.json

```
[
    {
        "username":"Al-Quran dan As-Sunnah",
        "image":"https://partalibra.files.wordpress.com/2017/11/download-3.jpg",
        "location":"Prabumulih, Indonesia",
        "diskripsi":"Developer React Native"
    },
    {
        "username":"Harta Riba",
        "image":"https://4.bp.blogspot.com/-fKeTOCEkHGA/WGRqtUjYpTI/AAAAAAAAHHc/bmelS2qqY6gNbd8LgD8W9U-B4m_sK_VGACK4B/s320/larangan-riba-dalam-al-quran-dan-sunnah.jpg",
        "location":"Medan,Indonesia",
        "diskripsi":"Developer Java"
    },
    {
        "username":"Apa itu Islam? ",
        "image":"https://2.bp.blogspot.com/-Re6W3Vb3FQU/WP1AX9oobtI/AAAAAAAAVis/ROZWrvzeFLYGg8pq15T5j2rlyv7s-ZIIgCLcB/s1600/Mulia%2Bdengan%2BIslam.jpg",
        "location":"Aceh, Indonesia",
        "diskripsi":" Node js"
    },
    {
        "username":"Kembali Kepada Al-Quran dan As-Sunnah",
        "image":"https://i.ytimg.com/vi/TTuJezU1nMw/maxresdefault.jpg",
        "location":"Bekasi, Indonesia",
        "diskripsi":"Node JS"
    },
    {
        "username":"Apa itu Tauhid",
        "image":"https://1.bp.blogspot.com/-rAs6oOzaXO0/WVXmGxJAdNI/AAAAAAAAhYU/e6SY4Wp4Uq0JM-RZDAqEIIDNWegpcOlXACLcBGAs/s320/quran%2Bsunnah.jpg",
        "location":"Manado, Indonesia",
        "diskripsi":"Php"
    }
]
```

## App.js

```
import React from 'react';
import {
    View, 
    Text,
    FlatList,
    StyleSheet,
    Image,
    TouchableOpacity
} from "react-native"

import Header from '../screen/Header' 
import Data from '../Config/Data.json' 


class Home extends React.Component {
    state = {
        Data
    }

    onButtomDetail=(dataItem) => {
        this.props.navigation.navigate('Search', {detil: dataItem })
    }
    render() {
        return(
           
            <View style={{flex:1}}>
                <Header titleHeader='Belajar Bareng Gan'/>
                {/* <ListData onPress={() => this.props.navigation.navigate('Search')}/> */}
                {/* <Text onPress={() => this.props.navigation.goBack()}> Home</Text> */}
                <FlatList
                    data={this.state.Data}
                    keyExtractor={(index, item) => index.toString()}
                    renderItem={({ index, item }) => {
                        return (
                            <View>
                                <TouchableOpacity onPress={() => this.onButtomDetail([`${item.username}`, `${item.location}`, `${item.image}`, `${item.diskripsi}`, `${item.artikel}`])}>
                                    <View style={styles.viewJudul}>
                                        <Text style={styles.judul}>{item.username}</Text>
                                        <Text style={styles.location}>{item.location}</Text>
                                    </View>
                                    <View style={styles.viewImages}>
                                        <Image source={{ uri: item.image}}  style={styles.styleImage} />
                                    </View>
                                    <View style={styles.diskripsi}>
                                        <Text>{item.diskripsi}</Text>
                                    </View>
                                </TouchableOpacity>
                            </View>
                        )
                    }}
                />
            </View>

        )
    }
}

export default Home

const styles = StyleSheet.create ({
    judul:{
        fontSize:25,
        color:'#000000',
        paddingLeft:5
    },
    viewImages:{
        justifyContent:'center',
        alignItems:'center'
    },
    styleImage:{
        height:200,
        width:'80%',
        marginBottom:4
    },
    location:{
        fontSize:10,
        marginBottom:20,
        paddingLeft:5

    },
    diskripsi:{
        borderBottomWidth:1,
        borderBottomColor:'green',
        paddingLeft:5

    }
})
```
## Search.js
```
import React from 'react';
import {
    View,
    Text,
    StyleSheet,
    Image,
    ScrollView
} from "react-native"

import Header from '../screen/Header'

class Search extends React.Component {
    render() {
        return (
            <View >
                <Header titleHeader='Pondok News' />
                <ScrollView>
                    <View style={styles.contantainer}>
                        <Text style={styles.titleArtikel} > {this.props.navigation.state.params.detil[0]}</Text>
                        <Text style={styles.lokasiPenulis} > {this.props.navigation.state.params.detil[1]}</Text>
                        <View style={styles.viewImages}>
                            <Image source={{ uri: this.props.navigation.state.params.detil[2] }} style={styles.ukuranGambar} />
                        </View>
                        <Text style={styles.tampilanArtikel} > {this.props.navigation.state.params.detil[4]}</Text>
                    </View>
                </ScrollView>
            </View>

        )
    }
}
const styles = StyleSheet.create({
    contantainer: {
        flex: 1,
        backgroundColor: '#fff'
    },
    titleArtikel: {
        fontSize: 25,
        color: '#000000',
    },
    lokasiPenulis: {
        fontSize: 10,
        marginBottom: 20,
        paddingLeft: 5
    },
    ukuranGambar: {
        height: 200,
        width: '80%',
        marginBottom: 4
    },
    viewImages: {
        justifyContent: 'center',
        alignItems: 'center'
    },
    tampilanArtikel: {
        fontSize: 15,
        textAlign: 'auto'
    }

})

export default Search
```
