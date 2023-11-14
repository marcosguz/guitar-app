<h1 align="center">Guitar App</h1>



```javascript
export function App() {
    const [currentTVShow, setCurrentTVShow] = useState();
    const [recommendationList, setRecommendationList] = useState([]);

    async function fetchPopulars() {
        try {
            const popularTVShowList = await TVShowAPI.fetchPopulars();
            if (popularTVShowList.length > 0) {
                setCurrentTVShow(popularTVShowList[0]);
            }
        } catch (error) {
            alert("Something went wrong wwhen fetching the popular tv shows");
        }
    }

    async function fetchRecommendations(tvShowId) {
        try {
            const recommendationListResp = await TVShowAPI.fetchRecommendations(tvShowId);
            if (recommendationListResp.length > 0) {
                setRecommendationList(recommendationListResp.slice(0, 10));
            }
        } catch (error) {
            alert("...");
        }
    }

    useEffect(() => {
        fetchPopulars();
    }, []);

    useEffect(() => {
        if (currentTVShow) {
            fetchRecommendations(currentTVShow.id);
        }
    }, [currentTVShow]);

    function updateCurrentTVShow(tvShow) {
        setCurrentTVShow(tvShow);
    }

    async function fetchSearchTVShow(title) {
        try {
            const searchResponse = await TVShowAPI.fetchSearchTVShow(title);
            if (searchResponse.length > 0) {
                setCurrentTVShow(searchResponse[0]);
            }
        } catch (error) {
            alert("...");
        }
    }

    return (
        <div
            className={s.main_container}
            style={{
                background: currentTVShow
                    ? `linear-gradient(rgba(0, 0, 0, 0.55), rgba(0, 0, 0, 0.55)),
             url("${BACKDROP_BASE_URL}${currentTVShow.backdrop_path}") no-repeat center / cover`
                    : "black",
            }}
        >
            <div className={s.header}>
                <div className="row">
                    <div className="col-4">
                        <Logo
                            title="Watowatch"
                            subtitle="Find a show you may like"
                            image={logoImg}
                        />
                    </div>
                    <div className="col-md-12 col-lg-4">
                        <SearchBar onSubmit={fetchSearchTVShow} />
                    </div>
                </div>
            </div>
            <div className={s.tv_show_details}>
                {currentTVShow && <TVShowDetail tvShow={currentTVShow} />}
            </div>
            <div className={s.recommended_shows}>
                {currentTVShow && <TVShowList onClickItem={updateCurrentTVShow} tvShowList={recommendationList} />}
            </div>
        </div>
    );
}
```

## About the project

<table width="100%">
    <tbody width="100%">
        <tr>
            <td rowspan=5 align="rigth">
                <img src="https://github.com/marcosguz/tv-show-adviser/assets/75583218/cff6a44b-739e-42a3-a199-7ba8bdddbe0f" width="500px">
            </td>
        </tr>
        <tr>
            <td align="justify">This web application is developed for educational purposes to implement code preprocessor. It is quite simple to use: you just have to choose the guitar you like and its information will be displayed.</td>
        </tr>
        <tr>
            <td align="justify">
				<a href="https://guitar-app-store.netlify.app">Guitar App</a>
			</td>
        </tr>
    </tbody>
</table>

## Developed with
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![SASS Badge](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=white)

## How to contribute?
Contributions are what make the open source community an amazing place to learn, inspire, and create. Any contribution you make is greatly appreciated.

1. Fork the project.
2. Create a feature branch: (git checkout -b features/amazing-feature).
3. Commit your changes: (git commit -m 'Add an Amazing Feature').
4. Upload your changes to the branch: (features/amazing-feature)
5. Open a pull request

## License
Distributed under the MIT license. See the `LICENSE` file for more information.

## Contact
Marcos Guzmán

<a href="https://www.linkedin.com/in/marcos-guzman-nazareno" target="blank">
      <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="Marcos"/>
</a>
<a href="https://twitter.com/marccosgz" target="blank">
      <img src="https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white" />
</a>

## Recognitions
- [Sass](https://github.com/sass/sass)
- [Marked](https://marked.js.org/)
