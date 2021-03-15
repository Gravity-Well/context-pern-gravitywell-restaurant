Uses local postgres

Database name as desired.

Tables

-- Table: public.restaurants

-- DROP TABLE public.restaurants;

CREATE TABLE public.restaurants
(
    id serial NOT NULL primary key,
    name character varying(50) COLLATE pg_catalog."default",
    location character varying(50) COLLATE pg_catalog."default",
    price_range integer NOT NULL,
    CONSTRAINT restaurants_price_range_check CHECK (price_range >= 1 AND price_range <= 5)
)


-- Table: public.reviews

-- DROP TABLE public.reviews;

CREATE TABLE public.reviews
(
    id bigserial NOT NULL primary key,
    restaurant_id bigint NOT NULL,
    name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    review text COLLATE pg_catalog."default" NOT NULL,
    rating integer NOT NULL,
    CONSTRAINT reviews_restaurant_id_fkey FOREIGN KEY (restaurant_id)
        REFERENCES public.restaurants (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT reviews_rating_check CHECK (rating >= 1 AND rating <= 5)
)

