## Cv
1. Mikryukov Nikita
2. Discord - NikitaAir#7657, telegram - NikitAirForce
3. My target is to become the best ios developer in the world))
I want to improve my studies in the field of ios development in this course. I am hungry for new knowledge. Sometimes I dream about how I develop applications because I constantly think about it
4. Skills : 
	1. Swift, C++, Js
	2. Realm,CoreData,Spring,SanpeKit,Almofire…..
	3. Mysql, HTML, CSS

5. Sample code
```swift
//

//  NetworkService.swift

//  AlbApp

//

//  Created by Никита on 24.02.2021.

//



import Foundation

import UIKit



enum ApiError : Error {

    case noData

}

//let check = Reachability()

var alert = SerachCollectionViewController()



class NetworkService {

    

    enum RequestType {

        case albumName(album: String)

        case aboutTheAlbum(album: String)

    }

    var onResult: ((Result<SearchResponse, Error>) -> Void)?

    

    func fetchAlbum (forRequestType requestType: RequestType) {

        var urlString = ""

        switch requestType {

        case .albumName(let album):

            urlString = "https://itunes.apple.com/search?term=\(album)&entity=album&limit=10"

            

        case .aboutTheAlbum(let album):

            urlString = "https://itunes.apple.com/lookup?id=\(album)&entity=song"

        }

        performRequest(withURLString: urlString)

    }

    

    

    fileprivate func performRequest(withURLString urlString: String) {

        

        guard let url = URL(string: urlString) else { return }

        let session = URLSession(configuration: .default)

        let task = session.dataTask(with: url) { data, response, error in

            if Reachability.isConnectedToNetwork(){

                if let httpResponse = response as? HTTPURLResponse {

                    print(httpResponse.statusCode)

                    if httpResponse.statusCode == 404 {

                        self.onResult?(.failure(ApiError.noData))

                        return

                    } else if httpResponse.statusCode != 200 {

                        self.onResult?(.failure(ApiError.noData))

                        return

                    }

                }

                

                if let data = data {

                    

                    let decoder = JSONDecoder()

                    do {

                        let objects = try decoder.decode(SearchResponse.self, from: data)

                        self.onResult?(.success(objects))

                    } catch let error as NSError {

                        self.onResult?(.failure(error))

                        print(error.localizedDescription)

                    }

                }else {

                    self.onResult?(.failure(ApiError.noData))

                    print("xxxxxxx")

                    return

                }

            } else{

                print("Internet Connection not Available!")

                self.onResult?(.failure(ApiError.noData))

                return

            }

        }

        task.resume()

    }

}
```

6. Мои проекты(все ссылки на Github):

	*  [Приложение по поиску музыкальных альбомов](https://github.com/97nik/AlbApp) 
	*  [Приложение по поиску фотографий по тегу](https://github.com/97nik/PictureColletion) 
	*  [Рик и Морти](https://github.com/97nik/ApiRickandMorti)  (парсинг Json)
	*  [BatAnimation](https://github.com/97nik/testAnimation2)  (анимация с помощью фреймворка Spring)
7.  Education 
	- Admiral Makarov State University of Maritime and Inland Shipping / Bachelor's degree graduated in 2019 / information systems and technology
	- Swiftbook course 
9. English level b1.  I go to spoken English twice a week
