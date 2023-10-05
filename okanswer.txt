package main

import (
	"encoding/json"
	"fmt"
)

const (
	ApiUrl      = "https://development.kpi-drive.ru/_api/facts/save_fact"
	AccessToken = "48ab34464a5573519725deb5865cc74c"
)

type Tag struct {
	Id           int    `json:"id"`
	Name         string `json:"name"`
	Key          string `json:"key"`
	ValuesSource int    `json:"values_source"`
}

type SuperTag struct {
	Tag   Tag    `json:"tag"`
	Value string `json:"value"`
}

// updated
type RequestData struct {
	Supertags []SuperTag `json:"supertags"`
	Limit     int        `json:"limit"`
}

type ResponseData struct {
	// Your data type here, based on server response
	// TODO: Unmarshal JSON onto this struct
}

func main() {
	requestData := RequestData{
		Supertags: []SuperTag{
			{
				Tag: Tag{
					Id:           2,
					Name:         "Клиент",
					Key:          "client",
					ValuesSource: 0,
				},
				Value: "Иванов И. И.",
			},
		},
		Limit: 1,
	}

	dataJSON, err := json.Marshal(requestData)
	if err != nil {
		fmt.Printf("Error creating JSON: %v\n", err)
		return
	}
	fmt.Printf("%s\n", dataJSON)
}
